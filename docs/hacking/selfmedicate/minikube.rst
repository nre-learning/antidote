Running selfmedicate on Minikube
================================

Self-Medicate Configuration options
-----------------------------------

.. warning::
    Currently, selfmedicate on Minikube only supports mac and linux. If you want to run this on Windows, please see
    :ref:`Running selfmedicate on Vagrant`

You can create a configuration file for selfmedicate, but it is not required.  It should be called "config"
and located in directory "$HOME/.antidote/"  Not all variables need to be specified.  The following variables
are supported::

    CPUS               - The number of CPUs minikube should run on.  (default: 2)
    MEMORY             - The amount of memory in megabytes minikube should run on. (default: 8192)
    VMDRIVER           - The hypervisor minikube should use (default: virtualbox)
    LESSON_DIRECTORY   - The location of the lesson directory.  (default: "../nrelabs-curriculum")
    MINIKUBE           - The path to the 'minikube' command. (default: "minikube", if installed on PATH)
    KUBECTL            - The path to the 'kubectl' command. (default: "kubectl", if installed on PATH)
    PRELOADED_IMAGES   - The list of images to be pre-loaded in advance. (default: "vqfx:snap1 vqfx:snap2 vqfx:snap3 utility")

Example::

    CPUS=4
    MEMORY=16384
    VMDRIVER=kvm2
    LESSON_DIRECTORY="$HOME/projects/nrelabs-curriculum"

.. NOTE::

   Minikube's `kvm2 VM driver
   <https://github.com/kubernetes/minikube/blob/master/docs/drivers.md#kvm2-driver>`_
   (set in VMDRIVER in the example above) is also supported when on
   Linux. It allows Minikube to run Kubernetes inside a qemu+kvm VM,
   which should offer better performance on Linux machines provided
   they support nested virtualization.

Install and Configure Prerequisites
-----------------------------------

The development environment runs within a virtual machine, so you'll need a hypervisor. We recommend
`Virtualbox <https://www.virtualbox.org/wiki/Downloads>`_ as it is widely supported across operating systems
as well as the automation we'll use to get everything spun up on top of it.

Next, you'll need minikube. This is by far the easiest way to get a working instance of Kubernetes
running on your laptop. Follow the `installation instructions <https://kubernetes.io/docs/tasks/tools/install-minikube/>`_
to install, but do not start minikube.  Make sure you install kubectl as well.  Instructions are on the same page.

.. note:: 

    The ``selfmedicate`` script starts a minikube VM with 8GB of RAM and 4 vCPUs by default. While this isn't a strict
    requirement, it's a highly advised minimum. Depending on the lessons you start, it can require quite a bit of system
    resources, especially if you start multiple lessons in parallel.

Self-Medicate in Minikube
---------------------------------

Now we are ready to run selfmedicate.  Please refer to :ref:`Starting Self-Medicate`