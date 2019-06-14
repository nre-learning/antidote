.. _contrib-platform:

Contributing to the Antidote Platform
=====================================

First, you should take a look at the :ref:`platform architecture documentation <architecture>`. You don't need to memorize it, but
it will give you valuable overview of the various components involved in the Antidote platform.

At a high level, the two primary areas of focus for the Antidote platform are:

- **`antidote-web <https://github.com/nre-learning/antidote-web>`_** - this is the web front-end for the platform. If you lean more
  towards front-end development, such as HTML, CSS, and Javascript, this repository is a good place to start.
- **`syringe <https://github.com/nre-learning/antidote-web>`_** - this is the "brains" of Antidote - the back-end orchestrator that
  is responsible for making everything work behind the scenes. If you've primarily worked with systems languages like Python or Go,
- **`antidote-ops <https://github.com/nre-learning/antidote-ops>`_** - this is where we do all the automation to make the project itself
  work. Here, we manage scripts and playbooks for doing release automation - that is, the workflows for actually releasing a version of
  the platform software. We also manage the NRE Labs site itself here - both automation for the infrastructure, as well as curriculum
  release automation. If you like automating things, this may be a good place for you to start.

The first thing you should do for any repository mentioned above that is of any interest to you, is to "Watch" it.
Any activity that takes place in this repo will generate a notification for you. You can control how you're notified in
your GitHub settings, but we recommend enabling email notifications. It's a great way to make sure you're at least aware
of what's going on. If you aren't interested, you can always just delete the email.

No matter your comfort level or expertise, we've made special efforts to provide avenues to becoming aquainted with the details
of the platform, and being able to contribute. Note that this doesn't have to mean "writing code". There are a number of valuable
ways for you to contribute that don't require you to be a developer, and we'll cover some of these below.

Feature Requests and Bug Reports
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The absolute easiest way to contribute is to use the platform and let us know about any problems you encounter, or ideas you have
about improving things. This can be as simple as providing feedback about your experience on the NRE Labs site, or with
the :ref:`curriculum development environment <selfmedicate>`.


- Testing the platform and opening bug reports


Pull Request Reviews
~~~~~~~~~~~~~~~~~~~~

I always open PRs as soon as I'm working on something,
  and try my best to push every commit as soon as I make it. Anyone and everyone is welome
  to make constructive questions or comments on any in-progress PR, you don't have to be
  a maintainer to do this. Asking questions about the platform or work that's happening on
  it is incredibly valuable on its own, and is often the best way to become more familiar with 
  the platform without any risk.

Starting Small
~~~~~~~~~~~~~~

https://github.com/nre-learning/antidote-ops/labels/complexity%3A%20low

- Issues in the repos. If you learn more towards web or front-end development, the complexity: low
  tag in antidote-web may interest you. If you like to work on back-end systems, the same tag in Syringe may
  interest you. These are feature enhancements or bugfixes that I've set aside for folks to learn the platform,
  that are relatively approachable - i.e. don't require you to know how everything works in order to satisfy them.

Support? ask questions via the :ref:`community forums <community-forums>`,