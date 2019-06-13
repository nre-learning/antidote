.. _lessonimages:

Lesson Endpoint Images
===================================

Antidote, and all of the lessons that it manages, runs on Kubernetes As a result, all lesson
:ref:`endpoints <toolbox-endpoints>`, including network devices, are executed from prebuilt
Docker images. This means that if you have a particular piece of software you wish to show,
you may need to build your own Docker image that's compatible with Antidote.

This document aims to help you understand when it's necessary to build your own image, as well as how to do it.
It's quite possible that you don't need to concern yourself with a custom Docker image at all. There are a few ways
to show content in a lesson that don't involve creating new Docker images on your own. The best way to get started
is to peruse the table below, identify what you're trying to do, and go to the corresponding section.

======================================  ============================================================
I want to...                            Go to...
======================================  ============================================================
Run some commands or scripts            See "Use an Existing Image"
Use a new library or simple tool        See "Extend an Existing Image"
Show a totally new tool or software     See "Create a New Image" 
======================================  ============================================================

Use an Existing Image
~~~~~~~~~~~~~~~~~~~~~

Putting your "stuff" (scripts, configs, etc) into a Docker image isn't the only way to get it into a lesson.
At this point, you probably know that Antidote lessons are defined with simple text files, and those files are stored in
a Git repository. What you might not know is that when a lesson is instantiated, the full directory that contained that lesson
in the Git repository is made available to each lesson endpoint.


Every endpoint that's instantiated in a lesson has that lesson's directory mapped to it, and all of its contents.



- If you just want to run a set of bash or Python commands, or you have a script you wish to show, you likely don't need to
  do anything beyond simply placing those files into the lesson directory, or putting a set of commands into a lesson guide.
  The ``utility`` image, for example, comes preloaded with Python and a bash shell, so can satisfy a lot of use cases here.
  You simply reference this image when defining an endpoint in your lesson definition, and any files you place in the lesson
  directory will be made available at runtime. In NRE Labs, this is the ``/antidote`` directory.


**TODO(mierdin):** Need to highlight existing images that should be considered before new images are created. List the popular images and describe them



Extend an Existing Image
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


- Sometimes you need to go a bit further, such as installing a dependency that doesn't exist in one of the primary images.
  For example, the ``utility`` image comes preinstalled with a number of Python libraries but naturally, the one you want might
  not be there. It might be easiest to simply add your library to the list of requirements in that image, rather than create your
  own.

There are also some images you should be aware of that are maintained by the Antidote project, meant to be re-used
as much as possible, to avoid image sprawl.



First, learn the basics of docker. Most of how an image is built in Antidote aligns with this. We just have a few additional requirements to keep in mind.

Use your own repos for the time being, but we will need the full source for your container image

What NOT to put in a container image. Generally we only want new images if we have to have them. Please consider if an existing image (include catalog) satisfies your requirement.
Building an image to include your script in it, is not a good reason to build a new image. Lessons will always have all of the lesson content mapped via folder redirection.
Most simple files can easily be stored in the lesson directory and made available at runtime.

Create a New Image
~~~~~~~~~~~~~~~~~~

While there are a few minor requirements you'll need to adhere to in order to build images for Antidote,
the vast majority of what you'll need to know is contained in any reasonable Docker tutorial, especially content that focuses
on building images. For now, start with tutorials like the ones below, and learn the basics of Docker images:

- `Docker: Getting Started <https://docs.docker.com/get-started/>`_
- `Dockerfile Best Practices <https://docs.docker.com/develop/develop-images/dockerfile_best-practices/>`_

Antidote isn't a container scheduler; it uses Kubernetes for the heavy lifting there. That means there's not a tremendous
amount of work to get a "regular" Docker image to work in Antidote. For the most part, a container that works outside
of Antidote will work just fine within Antidote.

The only opinions Antidote has about how you build your container images is nearly solely focused on how that container
can be communicated with at runtime.
What's required, is to make sure the image is able to talk to the Antidote processes in the expected way, so that
all of the lesson scheduling logic knows when a lesson is ready, and how to present that content to the learner.

To that end, there are a few minor requirements that every image must follow.

- At a minimum, a port must be opened, and something must respond to basic TCP connections.
- Any images meant to be used as type ``device`` or ``utility`` must be
  configured to listen for SSH connections on port 22 and support the credentials antidote/antidotepassword.

In addition to the technical requirements for running an image in Antidote, there are few additional procedural requirements
if you intend this image to be used within NRE Labs.

- All files necessary for building a lesson image must be included in the lesson directory. Lessons hosted on
  NRE Labs must use images built via our tooling. No external images will be used.


During a pull request, you can push images to your own docker hub account, but if you want us to run this content, we'll need
the container source, and we'll be incorporating it into our docker hub account for security purposes.

However, you should only propose a new image when totally necessary. In many cases, putting things like scripts or configs within the lesson directory is sufficient.





