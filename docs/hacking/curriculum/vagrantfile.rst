.. _selfmedicate-vagrant:

Vagrant Environment for Self-Medicate
=====================================

For maximum compatibility across operating systems, we have packaged a Vagrantfile with :ref:`selfmedicate`, so that
it can run in a consistent, properly configured virtual machine with all of the dependencies needed.

.. NOTE::

    Running Self-Medicate within this Vagrant environment is the only supported option today. Linux users
    may wish to run the Self-Medicate script directly, to bypass the first layer of virtualization.

    You're welcome to go this route, of course, but you'll be on your own. You'll also want to make sure
    Docker, ``kubectl`` and minikube are all installed.

Install and Configure Prerequisites
-----------------------------------

These instructions will spin up a virtual machine, so first, you'll need a hypervisor. We recommend
`Virtualbox <https://www.virtualbox.org/wiki/Downloads>`_ as it is widely supported across operating systems
as well as the automation we'll use to get everything spun up on top of it.

Next, you'll need Vagrant. Vagrant uses Boxes to easily install preconfigured VMs. Follow 
the `installation instructions <https://www.vagrantup.com/docs/installation/>`_ to install.

.. note:: 

    The Self-Medicate Vagrantfile starts a VM with 8GB of RAM and 2 vCPUs by default. While this isn't a strict
    requirement, it's a strongly advised minimum.

Once Vagrant is installed, there are a few more things you need to do before you start the VM.
Vagrant's `vagrant-hostsupdater <https://github.com/cogitatio/vagrant-hostsupdater>`_ plugin is used to
automatically update the hosts file with the antidote-local URL. Depending on your system settings, you
may be prompted to allow access to the hosts file.

Vagrant's `vagrant-vbguest <https://github.com/dotless-de/vagrant-vbguest>`_ plugin should be installed if
using virtualbox. This allows vagrant to mount the
`NRE Labs Curriculum <http://github.com/nre-learning/nrelabs-curriculum>`_.

You can install these plugins using the following commands:

.. CODE::

    vagrant plugin install vagrant-hostsupdater
    vagrant plugin install vagrant-vbguest

Starting Vagrant and Selfmedicate
---------------------------------

To test antidote in a virtual machine under Vagrant's control, run:

.. code::

    vagrant up

This will download a `slim Ubuntu 16.04 box <https://app.vagrantup.com/bento/boxes/ubuntu-16.04>`_ then a 
provisioner will install docker, minikube and kubectl into the vagrant vm. Next, the provisioner will
run the ``selfmedicate.sh start``

.. WARNING::

    Each of these steps are performed in sequence, and will wait for everything to finish before moving on to the
    next step. This script is designed to do as much work as possible up-front, so that your development experience
    can be as positive as possible. As a result, the first time you run this command can take some time. BE PATIENT.
    Also note that if you destroy your minikube instance, you'll need to redo all of the above. If you want to just
    temporarily pause your environment, see the section below on the ``vagrant suspend`` and ``vagrant resume`` subcommands.

Once this is done, the environment should be ready to access at the URL shown by the script.

Pausing and Resuming Vagrant
----------------------------

As mentioned above, if you destroy the minikube environment, you'll need to perform the ``start`` command all over again.
However, it would be nice to be able to stop the environment temporarily, and resume later without installing everything
over again from scratch.

Fortunately, the ``vagrant suspend`` and ``vagrant resume`` subcommands do just this for us. To stop/pause the environment, run:

.. code::

    vagrant suspend

To resume, run:

.. code::

    vagrant resume

The ``resume`` command is important to run, since this re-executes minikube with the optional arguments needed
by Antidote, so make sure to use this, rather than trying to use ``minikube start`` directly.

.. note:: 

    The vagrant suspend command saves the vm memory to disk. Below we have options to shutdown the vm.

Optionally, we can shutdown the VM by using ``vagrant halt`` and turn it back on by using ``vagrant up``.

.. code::

    vagrant halt

To turn back on, run:

.. code::

    vagrant up

Accessing the VM
----------------

To maintain an open connection to the VM, run:

.. code::

    vagrant ssh
