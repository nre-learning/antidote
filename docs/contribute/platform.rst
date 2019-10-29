.. _contrib-platform:

Contributing to the Antidote Platform
=====================================

First, you should take a look at the :ref:`platform architecture documentation <architecture>`. You don't need to memorize it, but
it will give you valuable overview of the various components involved in the Antidote platform.

At a high level, the two primary areas of focus for the Antidote platform are:

- `antidote-web <https://github.com/nre-learning/antidote-web>`_ - this is the web front-end for the platform. If you lean more
  towards front-end development, such as HTML, CSS, and Javascript, this repository is a good place to start.
- `syringe <https://github.com/nre-learning/syringe>`_ - this is the "brains" of Antidote - the back-end orchestrator that
  is responsible for making everything work behind the scenes. If you've primarily worked with systems languages like Python or Go,
- `antidote-ops <https://github.com/nre-learning/antidote-ops>`_ - this is where we do all the automation to make the project itself
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

There's a few ways to do this. One of the simplest is to simply make a post on the `community forums <https://community.networkreliability.engineering>`_
and let us know what you think. A maintainer will be along to get more information if needed, and may provide guidance on what else to do.

Second, you could :ref:`post a Github Issue <git-issues>` on the Github repository you think applies to your concern best. Same as with the community
forums, someone will be along to provide guidance from there..

Contributing your perspective, no matter your training, is just as valuable a contribution as writing code, so please don't shy away from this.
If you have constructive feedback, we want to hear it.

Pull Request Reviews
~~~~~~~~~~~~~~~~~~~~

If you want to start getting familiar with the platform, another easy way is to :ref:`watch the relevant Github repository <git-watching>`
for updates, such as new Pull Requests, and ask questions. Lots of platform developers open pull requests as soon as they start working
on a feature or a bugfix, which often gives a large window of time where the pull request is open and questions can be asked, even
on specific lines of code that changed.

Any constructive comments or questions here are not only appreciated, but it's often the best way to get insight into how the platform works,
as you're inserting yourself right into where the work is actually getting done, without having to write a single line of code yourself.
You don't have to be a platform developer or even consider yourself a developer at all to be curious and ask questions. We'd love to have you
and help you get more familiar with how things work within the Antidote platform.

Starting Small
~~~~~~~~~~~~~~

Okay - let's say you're ready and willing to contribute something more directly, but you're not sure where to start. Fear not - you're not alone.
This is one of the most challenging parts of any open source project - picking that first or second task that's challenging enough to teach you
something, but not so challenging that you have to spin your wheels for weeks before you feel like you've accomplished anything.

We've explicitly carved up Github issues in nearly every Antidote project repository just for you. Take a look at the :ref:`Git section
of these docs <git-lowhanging>` where you'll find a system of labeling issues by complexity, so you can see at-a-glance which issues have
been identified for the express purpose of getting started with the project.

Going Big
~~~~~~~~~

For complex features, especially those that span across the various component projects to the Antidote platform,
you'll be required to create a blueprint in the `proposals <https://github.com/nre-learning/proposals/tree/master/blueprints>`_
repo. This gives needed structure for the effort you have in mind, and gives others a chance to get involved.

There are no hard rules on when a blueprint is required, but please be prepared to do this if a maintainer asks
in order to move things forward. There are also no rules on what should be *in* a blueprint, but it should minimally
answer the following:

- What is the problem you're trying to solve? How will this solve that problem?
- What components of Antidote (and how) will this need to touch?
- What is the detailed design of the feature in it's ultimate state?
- What are the discrete steps (each step being its own PR) we will need to take to accomplish this feature. If
  separate steps, how will we ensure project stability while the work is in progress?

Blueprints aren't meant to be a super formal, heavy-handed process for everyone to go through before they can
do anything - ideally they'll only be used for the really complicated ideas as the project moves out of the "alpha"
stage, and will help keep everyone abreast of the big ideas and how the work will get done - providing space for
everyone to contribute the way they want to.
