Lessons
============================

Antidote is a platform for bringing otherwise complicated technical learning material to the masses,
by taking care of the complexity behind the scenes, out of sight of the learner.
To that end, there are a variety of tools we make available to you, the lesson author / teacher
to make this possible.

.. image:: /images/toolbox.png
   :scale: 30 %
   :align: center

Some tools are designed to make things easier to teach, others makes things easier
to learn, other things do both. Please read through this portion of the
documentation so you don't miss out on any useful tools you can leverage
to really make your content stand out.

.. toctree::
   :maxdepth: 1

   endpoints.rst
   connections.rst
   guides.rst
   autoconfiguration.rst
   iframe.rst
   verification.rst

Lessons are the quintessential curriculum resource.



When syringe starts, it looks for lesson definitions within the configured curriculum directory,
loads them into memory, and serves them directly via its API.

.. warning::
    The way that lesson definitions are put together is still a work-in-progress.
    Be prepared for changes to the below information, as we improve Syringe and
    make it (hopefully) easier to put these lesson files together.

These lesson definitions are written in YAML. A very simple example is shown below. This file describes a very
simple lesson in two parts, with a single linux container for interactivity:

.. code:: yaml

  ---
  lessonName: Introduction to YAML
  lessonId: 14
  category: fundamentals
  tier: prod
  prereqs:
    - 22  # Python
  description: YAML is a human friendly data serialization standard. In this lesson, we'll explore the basics of YAML, and prepare for using it in a myriad of automation use cases.
  slug: YAML
  tags:
  - YAML
  - data modeling
  - data model

  utilities:
  - name: linux1
    image: antidotelabs/utility

  stages:
    - id: 1
      description: Lists
    - id: 2
      description: Dictionaries (key/value pairs)


A more complicated example adds network devices to the mix. This not only adds images to the file, but
we also need to add a list of connections for Syringe to place between our network devices, as well as
configurations to apply to each device at each lesson stage:

.. code:: yaml

  ---
  lessonName: Network Unit Testing with JSNAPY
  lessonId: 12
  category: tools
  lessonDiagram: https://raw.githubusercontent.com/nre-learning/antidote/master/lessons/lesson-12/lessondiagram.png
  tier: prod
  prereqs:
    - 14  # YAML
    - 23  # Linux
  description: Unit testing your network devices is one of the fundamental building blocks to CI/CD for networking. In this lesson, we'll explore the use of an open source tool - JSNAPy - for doing just this with Junos devices.
  slug: JSNAPy
  tags:
  - jsnapy
  - test
  - unit test
  - testing

  utilities:
  - name: linux1
    image: antidotelabs/utility

  devices:
  - name: vqfx1
    image: antidotelabs/vqfx:snap1
  - name: vqfx2
    image: antidotelabs/vqfx:snap2
  - name: vqfx3
    image: antidotelabs/vqfx:snap3

  connections:
  - a: vqfx1
    b: vqfx2
  - a: vqfx2
    b: vqfx3
  - a: vqfx3
    b: vqfx1

  stages:
    - id: 1
      description: No BGP config - tests fail

    - id: 2
      description: Correct BGP config - tests pass

