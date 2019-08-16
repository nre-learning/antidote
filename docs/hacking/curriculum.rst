.. _selfmedicate:

Hacking on the Curriculum
=========================

If you want to contribute some lessons, you'll probably want to find a way to run them locally
yourself before opening a pull request. Or maybe you're looking to show some automation demos
in an environment that doesn't have internet access (hello federal folks). If any of this describes
you, you've come to the right place.

The antidote project is meant to run on top of Kubernetes. Not only does this provide a suitable
deployment environment for the Antidote platform itself, it also allows us to easily spin up additional
compute resources for running the lessons themselves. To replicate the production environment at
a smaller scale, such as on a laptop, we use "`minikube <https://github.com/kubernetes/minikube>`_". This is a single-node Kubernetes cluster
that is fairly well-automated. This means you can do things like run demos of Antidote lessons
offline, or use this as your development environment for building new lessons.

The `antidote-selfmedicate <https://github.com/nre-learning/antidote-selfmedicate>`_ tool is a set of scripts
that use minikube to deploy a full functioning Antidote deployment on your local machine.

.. NOTE::

    This section discusses technical steps for running Antidote locally for the purposes of editing or adding to
    a curriculum. See :ref:`here <contrib-curriculum>` for instructions on how to contribute your changes or additions
    to the flagship NRE Labs curriculum.

Preparing the Environment
-------------------------
    
Open a terminal window.  Create, then enter the directory for the selfmedicate environment and curriculum lessons::

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

    **Please remember** that changes are being made to this repository all the time. If you encounter issues,
    the very first thing you should try before you open an issue is to make sure you have the latest copy of
    this repository by doing a ``git pull`` on the master branch.

Cannot connect to the Web Front-End
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

It's likely that the pods for running the Antidote platform aren't running yet. Try getting the current pods:

.. code::

    ~$ kubectl get pods
    NAME                                        READY   STATUS    RESTARTS   AGE
    antidote-web-99c6b9d8d-pj55w                2/2     Running   0          12d
    nginx-ingress-controller-694479667b-v64sm   1/1     Running   0          12d
    syringe-fbc65bdf5-zf4l4                     1/1     Running   4          12d

You should see something similar to the above. The exact pod names will be different, but you should see the same
numbers under the ``READY`` column, and all entries under the ``STATUS`` column should read ``Running`` as above.

In some cases the ``STATUS`` column may read ``ContainerCreating``. In this case, it's likely that the images for each pod
is still being downloaded to your machine. You can verify this by "describing" the pod that's not ``Ready`` yet:

.. code::

    kubectl describe pods -n=kube-system kube-multus-ds-amd64-ddxqc
    Name:               kube-multus-ds-amd64-ddxqc
    ....truncated....
    Events:
    Type    Reason     Age   From               Message
    ----    ------     ----  ----               -------
    Normal  Scheduled  19s   default-scheduler  Successfully assigned kube-system/kube-multus-ds-amd64-ddxqc to minikube
    Normal  Pulling    17s   kubelet, minikube  pulling image "nfvpe/multus:latest"

In this example, we're still waiting for the image to download - the most recent event indicates that the image is being pulled.
The ``selfmedicate.sh`` script has some built-in logic to wait for these downloads to finish before moving to the next step,
but in case that doesn't work, this can help you understand what's going on behind the scenes.

If you're seeing something else, it's likely that something is truly broken, and you likely won't be able to get the environment
working without some kind of intervention. Please `open an issue on the antidote-selfmedicate repository <https://github.com/nre-learning/antidote-selfmedicate/issues/new>`_
with a full description of what you're seeing.

Lesson Times Out While Loading
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Let's say you've managed to get into the web front-end, and you're able to navigate to a lesson, but the lesson just
hangs forever at the loading screen. Eventually you'll see some kind of error message that indicates the lesson timed
out while trying to start.

This can have a number of causes, but one of the most common is that the images used in a lesson failed to download within
the configured timeout window. This isn't totally uncommon, since the images tend to be fairly large, and on some internet
connections, this can take some time.

There are a few things you can try. For instance, ``kubectl describe pods <pod name>``, as used in the previous section,
can tell you if a given pod is still downloading an image.

We can also use the ``minikube ssh`` or ``vagrant ssh`` command to send commands into the minikube VM and see the results. For instance, to
check the list of docker images that have been successfully pulled:

If :ref:`Running selfmedicate on Minikube`:

.. code::

    minikube ssh docker image list

If :ref:`Running selfmedicate on Vagrant`:

.. code::

    vagrant ssh docker image list

This is the same as running ``docker image list``, but it's done from inside the minikube VM for you. Similarly, if you wanted
to manually pull an image ahead of time, you could run ``minikube ssh docker image pull <image>``.

.. note::

  The ``selfmedicate`` script downloads the most common images in advance to try to reduce the likelihood of this issue, and to
  generally improve the responsiveness of the local environment. However, it can't do this for all possible images you might want
  to use. If you know you'll use a particular image commonly, consider adding it to the ``selfmedicate`` script, or manually
  pulling it within the minikube environment ahead of time.
