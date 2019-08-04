.. _lessonimages:

Endpoint Images
===================================

Antidote, and all of the lessons that it manages, runs on Kubernetes. As a result, all lesson
:ref:`endpoints <endpoints>`, including network devices, are executed from prebuilt
Docker images. This means that if you have a particular piece of software you wish to show,
you may need to build your own Docker image that's compatible with Antidote. As the default for Antidote
(and is enforced in NRE Labs) is to disable internet access while a lesson is running, lessons must be
self-contained in order to work properly and prebuilt Docker images are key to accomplishing this.

This document aims to help you understand when it's necessary to build your own image, as well as how to do it.
It's quite possible that you don't need to concern yourself with a custom Docker image at all. There are a few ways
to show content in a lesson that don't involve creating new Docker images on your own.

If you're looking to run some commands or scripts, or maybe a new library or simple tool that's not currently supported
by the existing curriculum, please consider reading the first section below titled
:ref:`"Use or Extend an Existing Image" <images-use-extend>`.
If you need to show some totally new software or tool that requires a more formal installation process, continue to
:ref:`"Create a New Image" <images-create>`.

.. _images-use-extend:

Use or Extend an Existing Image
-------------------------------

Putting your "stuff" (scripts, configs, etc) into a Docker image isn't the only way to get it into a lesson.
At this point, you probably know that Antidote lessons are defined with simple text files, and those files are stored in
a Git repository. What you might not know is that when a lesson is instantiated, the full directory that contained that lesson
in the Git repository is made available to each lesson endpoint.

Every endpoint that's instantiated in a lesson has that lesson's directory mapped to it, and all of its contents.
If you just want to run a set of bash or Python commands, or you have a script you wish to show, you likely don't need to
do anything beyond simply placing those files into the lesson directory, or putting a set of commands into a lesson guide.

The ``utility`` image, for example, comes preloaded with Python and a bash shell, so can satisfy a lot of use cases here.
You simply reference this image when defining an endpoint in your lesson definition, and any files you place in the lesson
directory will be made available at runtime to the configured directory. In NRE Labs, this is the ``/antidote`` directory.

.. NOTE::

    This location is controlled by Syringe and configured using the ``SYRINGE_LESSON_REPO_DIR`` environment
    variable. See :ref:`Syringe configuration <syringe-config>` for more details.

There are some "common" images you might consider using before building your own:

``utility``
  ===========  =================================================================
  **Usage:**   ``image: antidotelabs/utility``
  **Source:**  https://github.com/nre-learning/nrelabs-curriculum/tree/master/images/utility
  ===========  =================================================================

    The ``utility`` image is a sort of "junk drawer". It has some basic things installed, like Python and a bunch of
    network automation related packages, and assorted other tools that are useful to have. The main intent behind this
    image was to provide a basic Linux CLI to launch into other things from. It has a basic security configuration to run
    an SSH server so that Syringe can get CLI access to it.

    Generally if you're looking to show something using a Linux CLI, and the "thing" you want to show is either easily
    added to this image, or shown via files in the lesson directory, this image will be a good fit.

``vqfx-snap<X>``
  ===========  =================================================================
  **Usage:**   ``image: antidotelabs/vqfx-snap1``
  **Source:**  https://github.com/nre-learning/nrelabs-curriculum/tree/master/images/vqfx
  ===========  =================================================================

  The ``vqfx-snap1`` image takes some shortcuts in order to boot quickly. A QEMU snapshot was taken after initial boot
  and initial configuration, and saved to the disk image.

  We have built three images using this process, which are accessible using the following image refs:

  - ``antidotelabs/vqfx-snap1``
  - ``antidotelabs/vqfx-snap2``
  - ``antidotelabs/vqfx-snap3``

  For some reason, while this snapshotting does wonders for boot speed, it doesn't allow us to be able to
  change the MAC addresses post-boot. This is why we built three, to give you up to three to use in a topology.
  Note that we're very aware this is not ideal, and we're working hard to get a better vqfx image in place that
  boots quickly and doesn't have these drawbacks. Contributions welcome!

.. NOTE::

    Previous versions of these docs included a listing for ``vqfx-full`` or ``container-vqfx``. We have removed those for
    now, as those are still not ready for primetime. In the very near future, we're hoping to have a single vqfx image that
    is useful across the board, that doesn't have the drawbacks of the snapshotted version.

Sometimes you need to go a bit further than what the current images offer, such as installing a dependency that
doesn't exist in one of the primary images. For example, the ``utility`` image comes preinstalled with a number
of Python libraries but naturally, the one you want might not be there. It might be easiest to simply add your
library to the list of requirements in that image, rather than create your own. In this case, adding the necessary
lines to the existing source Dockerfile or supporting files is all you need to do.

.. _images-create:

Create a New Image
------------------

Okay, so you've decided you need to create a totally new image. The good news is that there is a ton of material
out there to help you do this. While there are a few minor requirements you'll need to adhere to in order to build images for Antidote,
the vast majority of what you'll need to know is contained in any reasonable Docker tutorial, especially content that focuses
on building images. For now, start with tutorials like the ones below, and learn the basics of Docker images:

- `Docker: Getting Started <https://docs.docker.com/get-started/>`_
- `Dockerfile Best Practices <https://docs.docker.com/develop/develop-images/dockerfile_best-practices/>`_
- `Interactive Katacoda Lesson on Docker <https://www.katacoda.com/courses/docker/2>`_

Antidote isn't a container scheduler; it uses Kubernetes for the heavy lifting there. That means there's not a tremendous
amount of work to get a "regular" Docker image to work in Antidote. In general, a container that works outside
of Antidote will work just fine within Antidote.

The only exception to this rule is that the image supports anything configured within the
:ref:`Endpoints <endpoints>` and :ref:`Presentations <toolbox-presentation>` sections in your lesson definition. This is because Antidote
needs to be able to reach your running container over the network in order to provide access See the
:ref:`Presentations options documentation <presentation-options>` for more details on how your Endpoint image should support these options.

Images are automatically built using our back-end CI/CD workflows, and require a Makefile to be put in place that supports
a particular way of being called. For each image directory in a curriculum, the build process runs the following command:

.. CODE::

  make docker

All of the steps needed to build this image must be done automatically using that command. In addition, the ``TARGET_VERSION``
environment variable must be used by your Makefile to tag your image. This mustd efault to ``latest``, but can be
overridden by our build process, by calling the Makefile like so:

.. CODE::

  TARGET_VERSION=v0.4.0 make docker

This will result in the image in question being tagged with ``v0.4.0``. See
`here <https://github.com/nre-learning/nrelabs-curriculum/tree/master/images/utility/Makefile>`_ for an example of a Makefile
that supports the required options and builds and pushes the docker container automatically.

In addition to the technical requirements for running an image in Antidote, there are few additional procedural requirements
if you intend this image to be used within NRE Labs. First, for all NRE Labs contributions, the full source of the image (i.e. Dockerfile
and any other files referenced by it) must be contributed in a Pull Request so that we can build it within our infrastructure
and host it in the ``antidotelabs`` docker hub repository. This is a good idea for a bunch of reasons, especially
operational and security best practices.

In addition, if your image requires large files, (pretty much anything over 10MB) such as virtual machine disks or ISOs, you should add a step to your Dockerfile
to download those files from their original location, preferably with integrity verification using SHA256 hash or similar. If for some reason that's not
possible, :ref:`get in touch <community>` with us to discuss alternatives.

The ``image`` field of a lesson definition is passed directly to the underlying Kubernetes cluster. This means anything you can "docker pull"
from there can be placed in your lesson definition. This means if you are running your own version of Antidote, you can host your own docker
image repository just fine. In fact, even if you are aiming to contribute the lesson to the NRE Labs curriculum, this is the best way to build
and work on your images prior to opening a Pull Request. When you open a pull request that includes a new image, we'll make sure the
``images`` reference gets corrected before going live. Until then, you can use any location that suits you.
