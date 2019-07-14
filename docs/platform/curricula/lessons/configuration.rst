.. _toolbox-config:

Endpoint Configuration
======================

One of the best attributes of the Antidote platform is that it takes on as much complexity as is needed
on the back-end in order to provide a seamless learning experience to the user on the front-end. A big part
of this is the ability to automatically configure all lesson endpoints to fit the scenario being used to
teach a concept, so that when the learner is ready to take on a subject, they aren't distracted by fiddling
with configurations to "prep" the lesson.

Much of this advantage is gleaned from the fact that all Endpoints are started from Docker images, which
are cryptographically guaranteed to start the same way each time. All Endpoint software dependencies,
configurations, scripts, etc. are built right into the image. However, it's not always possible to put
**everything** into this image at build time. For instance, a network device can be built as a Docker
image, but depending on the Lesson or Stage, might have wildly different configurations, in order to
teach a particular concept. For this, Antidote offers the ability to configure Endpoints dynamically once
they're started from their base image.

.. NOTE::
    Don't overdo it with endpoint configuration. The fact that Antidote is powered by containers which
    are cryptographically guaranteed to start from the same base image each time is a huge advantage and
    it's useful to bake configurations into the container image wherever possible. So, use the configuration
    options below, but in proper balance with an already fairly functional base image configuration.


To accomplish this configuration, the Antidote project maintains a ``configurator`` image, which has all of the necessary
prerequisites for performing Endpoint configuration. When Antidote needs to perform a configuration for lesson Endpoints,
such as when a lesson is initially loaded, or when the user is navigating to a new Stage, Antidote will spin up one
configuration pod per lesson endpoint to perform the relevant configuration steps, and will populate those pods
with a few useful environment variables that can be consumed by the configuration scripts defined by the lesson
author. They are described below:

======================================  ============================================================
SYRINGE_TARGET_HOST                     Set to the IP address of the endpoint. Useful because this is always dynamic.
ANSIBLE_HOST_KEY_CHECKING               Set to "False" because I'm lazy and this is not a production environment.
======================================  ============================================================

The source for the ``configurator`` image is located in the
`nrelabs-curriculum <https://github.com/nre-learning/nrelabs-curriculum/tree/master/images/configurator>`_
repository, and is what's used as the runtime environment for all configuration options. The options below
are limited to what's been installed in this image. So, if you wish to use a Python library or Ansible module
that's not present, you may be able to add it to this image. If widely applicable enough, we'll consider adding
it for everyone.

Endpoints are individually configured on a per-stage basis, and the Antidote platform provides several
mechanisms for accomplishing this, so lesson builders have options when it comes to configuring their Endpoints.

Specifying which configuration type you want to use for your endpoint is fairly straightforward, but there are
some underlying implications you should be aware of for each option, which we'll explain below.

Configuration Options
~~~~~~~~~~~~~~~~~~~~~

NAPALM
  **Usage:** ``configurationType: napalm-<driver>``

  One of the most popular use cases for configuring endpoints between stages is putting a network configuration
  into place that's relevant to the concepts being taught. You may want to have three virtual switches in a topology
  but based on the stage being viewed, the configuration might need to change. This is a very common scenario.

  Rather than write a custom Python script or Ansible playbook to simply load a config onto a network device,
  you can use the NAPALM configuration option shown here.

  To use this option, you need to specify a specially formatted ``configurationType`` value. This configuration option uses
  the ``napalm-<driver>`` syntax, where ``<driver>`` is the name of the `NAPALM driver <https://napalm.readthedocs.io/en/latest/support/#general-support-matrix>`_
  you wish to use. For instance, if the network device is running Junos, you'll specify ``configurationType: napalm-junos``.
  Anything after the hyphen is passed directly to NAPALM, so make sure you're using the right driver name.

  This configuration option will look for a file with the extension ``.txt``, which is named identically to the endpoint
  you wish to configure. For instance, a configuration for a device called ``vqfx1`` will be named ``vqfx1.txt``.
  A configuration file must exist for every endpoint that uses this option, in the config directory of every stage.

  Some network images use IP masquerade (NAT) for the management interface, which means you don't need to worry about the
  IP configuration for this interface - it's usually static per that image's configuration. The "outer" address is assigned
  automatically from a container level, and the inner virtual machine doesn't need to worry about it. However, in some cases,
  NAT is not used, and you need to be able to leverage the environment passed to the configuration pod to ensure you
  get the right address. If this describes you, read on. If not, you can safely ignore the next paragraph.

  As mentioned previously, all configuration pods are started with the environment variable ``SYRINGE_TARGET_HOST``
  set to the IP address of the endpoint within Kubernetes. This is useful because this is assigned dynamically and you
  might want to use this in your configuration. So, instead of applying the configuration directly to the device,
  the configuration environment will first render the source file as a Jinja2 template. If you reference the variable
  ``mgmt_addr`` anywhere in the config using Jinja syntax (e.g. ``{{ mgmt_addr }}``), it will be replaced with the
  IP address of the management interface. The subnet mask of this interface must be configured according to the CNI
  configuration in place. Normally this is a ``/12``.

  This will use NAPALM's ``load-merge`` function to load the resulting config onto the device, and commit it.

Python
  **Usage:** ``configurationType: python``

  If you wish, you can use a custom Python script to make the necessary configuration changes.
  If you specify the above ``configurationType`` value, you'll need to make sure that for every
  endpoint that uses this option, a file named ``<endpoint>.py`` is present in the config
  directory for each stage.

Ansible
  **Usage:** ``configurationType: ansible``

  If you wish, you can use an Ansible playbook to make the necessary configuration changes.
  If you specify the above ``configurationType`` value, you'll need to make sure that for
  every endpoint that uses this option, a file named ``<endpoint>.yml`` is present in the config
  directory for each stage for every endpoint that uses this option.

