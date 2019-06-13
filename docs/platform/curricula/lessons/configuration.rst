.. _toolbox-config:

Endpoint Configuration
======================

One of the best attributes of the Antidote platform is that it takes on as much complexity as is needed
on the back-end in order to provide a seamless learning experience to the user on the front-end. A big part
of this is the ability to automatically configure all lesson endpoints to fit the scenario being used to
teach a concept, so that when the learner is ready to take on a subject, they aren't distracted by fiddling
with configurations to "prep" the lesson.

Endpoints are individually configured on a per-stage basis, and the Antidote platform provides several
mechanisms for accomplishing this, so lesson builders have Options

.. NOTE::
    Don't overdo it with endpoint configuration. The fact that Antidote is powered by containers which
    are cryptographically guaranteed to start from the same base image each time is a huge advantage and
    it's useful to bake configurations into the container image wherever possible. So, use the configuration
    options below, but in proper balance with an already fairly functional base image configuration.

Antidote will spin up one configuration pod per lesson endpoint to perform the relevant
configuration steps, and will populate those pods with a few useful environment variables that can be consumed
by the configuration scripts defined by the lesson author. They are described below:

======================================  ============================================================
SYRINGE_TARGET_HOST                     Set to the IP address of the endpoint. Useful because this is always dynamic.
ANSIBLE_HOST_KEY_CHECKING               Set to "False" because I'm lazy and this is not a production environment.
======================================  ============================================================



Configuration Options
~~~~~~~~~~~~~~~~~~~~~

NAPALM
  **Usage:** ``configurationType: napalm-<driver>``


  In previous versions of the Antidote platform, this was the only option. It's a fairly easy way to
  get a config file from the repo onto a network device. While we've made improvements to this

  This doesn't just use NAPALM, but also does the templating thing with the env var

Python
  **Usage:** ``configurationType: python``

  The term is a one-line phrase, and the
  definition is one or more paragraphs or
  body elements, indented relative to the
  term. Blank lines are not allowed
  between term and definition.


Ansible
  **Usage:** ``configurationType: ansible``

  The term is a one-line phrase, and the
  definition is one or more paragraphs or
  body elements, indented relative to the
  term. Blank lines are not allowed
  between term and definition.



