Hacking on the Curriculum
=========================

This section discusses technical steps for working on the NRE Labs curriculum. Once you've made your changes,
the :ref:`NRE Labs curriculum contribution docs <contrib-curriculum>` contain instructions on how to
contribute your changes or additions upstream.

If you want to contribute to the curriculum, you'll probably want to find a way to run them locally
yourself before opening a pull request. The `antidote-selfmedicate <https://github.com/nre-learning/antidote-selfmedicate>`_ tool is a set of scripts
that use minikube to deploy a full functioning Antidote deployment on your local machine.

Preparing the Environment
-------------------------

Open a terminal window.  Create, then enter the directory for the selfmedicate environment and curriculum lessons:

.. CODE::

    mkdir ~/antidote-local && cd ~/antidote-local
 
Next, if you're working with the development environment, you also may be looking to contribute to the NRE Labs
curriculum. If so, follow the :ref:`Antidote Git instructions <antidote-git>` to fork and clone the
`nrelabs-curriculum <http://github.com/nre-learning/nrelabs-curriculum>`_ repository to this directory. Not only
is this required for this development environment to work (it needs a curriculum to run), it also sets you up
to contribute to the curriculum later.

Next, all of the scripts and kubernetes manifests for running Antidote within minikube are located in the
`antidote-selfmedicate <https://github.com/nre-learning/antidote-selfmedicate>`_ repository. Simply clone
and enter this repository::

    cd ~/antidote-local && git clone https://github.com/nre-learning/antidote-selfmedicate && cd antidote-selfmedicate

.. WARNING::

    **Please remember** that changes are being made to these repositories all the time. If you encounter issues,
    the very first thing you should try before you open an issue is to make sure you have the latest copy of
    this repository by doing a ``git pull`` on the master branch.

Next, follow the links below to use the ``antidote-selfmedicate`` repository you cloned above to spin up a local
copy of Antidote so you can work on curriculum content.

.. toctree::
   :maxdepth: 1

   selfmedicate.rst
   vagrantfile.rst