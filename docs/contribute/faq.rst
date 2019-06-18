.. _curriculum-tips:

Tips and FAQs
=============


How can I stand up a development environment to test my curriculum contributions?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The :ref:`selfmedicate <selfmedicate>` documentation is exactly what you need. This
environment allows you to spin up a local instance of Antidote on your own machine, and map your
curriculum into it so you can see your changes live without having to open a pull request right away.

How are you running network devices in this thing?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Everything in Antidote is executed in Kubernetes, so everything has to be a container. On the surface, this
may seem like a barrier to being able to run virtual networking images, which are commonly available as
virtual machines. Indeed, a common misconception is that the two models are mutually exclusive, but
they're not.

At the end of the day, a container is just a highly configured process, and QEMU can execute
virtual machines easily with a single command. We build all of this into a container image, so
that in essence, when the container is started, the virtual machine is started as well.

See :ref:`architecture <architecture>` for more details on this and other aspects of images
within Antidote.

Do you only support Junos?
~~~~~~~~~~~~~~~~~~~~~~~~~~

This is a common question we get because the only image currently in use in the NRE Labs curriculum
is the vQFX image, and of course Juniper is paying the cloud bills for the NRE Labs site, so this question
is a fair one.

Bottom line is, there's no architectural restriction against running other images. In fact, the platform was
built from day one to be multivendor, and not just in the fact we can run the image, but also in how it's
incorporated into the true value of the platform, such as autoconfiguration between labs.

The technical requirement is that the network device is accessible via SSH for terminal access with the
appropriate credentials and packaged within a docker container. We're already using very flexible tools for doing
inter-stage configuration, so we're ready to use other vendor kit from the get-go; it's just a matter
of getting vendors to contribute their image. Juniper has done this as an early example, but any other
vendor that is willing to abide by the Code of Practice (coming soon) is welcome to
participate in the project.

In short, we've put the right technical pieces in place to make it possible, now we're working on getting
other vendors to contribute images to be used in the platform.

How do I get my "stuff" into a lesson?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It's quite rare to have a lesson in mind that doesn't also include some kind of custom "thing".
This could be a simple script you wrote or downloaded and wish to show it in your lesson,
configuration or data files used by an application, or full-blown software you'd like to be
installed and running or available within the environment. At the end of the day,
your goal is to get this "stuff" into your lesson definition.

In the **vast majority of cases**, the best way to do this is simply to store those files in the
curriculum repo within your lesson directory. In    

it's a matter of just putting it in your lesson directory. The entire curriculum is mapped via volume
to every container that runs in a lesson, so just by having those files in that directory, you'll have access to them at runtime.

You can also create a docker image that follows the :ref:`image <lessonimages>` guidelines
if you want a more complicated software installation to be present.
