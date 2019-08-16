Running selfmedicate on Vagrant
===============================

Install and Configure Vagrant Prerequisites
-------------------------------------------

The development environment runs within a virtual machine, so you'll need a hypervisor. We recommend
`Virtualbox <https://www.virtualbox.org/wiki/Downloads>`_ as it is widely supported across operating systems
as well as the automation we'll use to get everything spun up on top of it.

Next, you'll need vagrant. Vagrant uses Boxes to easily install preconfigured VMs. Follow 
the `installation instructions <https://www.vagrantup.com/docs/installation/>`_ to install.

.. note:: 

    The vagrantfile starts a VM with 8GB of RAM and 2 vCPUs by default. While this isn't a strict
    requirement, it's a highly advised minimum. Depending on the lessons you start, it can require quite a bit of system
    resources, especially if you start multiple lessons in parallel.


Vagrantfile Prerequisites
-------------------------

Vagrant's `vagrant-hostsupdater <https://github.com/cogitatio/vagrant-hostsupdater>`_ is used to automatically update the hosts
file with the antidote-local URL.  Depending on your system settings, you may be prompted to allow access to the hosts file.

Vagrant's `vagrant-vbguest <https://github.com/dotless-de/vagrant-vbguest>`_ should be installed if using virtualbox. This allows
vagrant to mount the `nrelabs-curriculum <http://github.com/nre-learning/nrelabs-curriculum>`_.

vagrant plugin install vagrant-hostsupdater
vagrant plugin install vagrant-vbguest

Starting Vagrant and Selfmedicate
---------------------------------

Please see :ref:`About Self-Medicate` for details about the ``selfmedicate.sh`` script.

The vagrantfile calls ``selfmedicate.sh start`` during is provision step.  To initialize antidote, run
``vagrant up``

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

By using ``vagrant ssh`` we can access the vm to run the troubleshooting commands found on
:ref:`Troubleshooting Self-Medicate`.

To maintain an open connection to the VM, run:

.. code::

    vagrant ssh

Alternatively we can send an individual command such as the syringe lesson reload:

.. code::

    vagrant ssh -c "$HOME/selfmedicate.sh reload"