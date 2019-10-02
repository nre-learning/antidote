.. _hacking-platform:

Hacking on the Platform
=======================

There are two main components to the Antidote platform:

- Antidote-web
- Syringe

In this document, we'll explain what it takes to work on the code. Note that
this document deals only with the technical steps for getting started working on the various
Antidote subprojects. Please read the :ref:`platform contribution docs <contrib-platform>`
for instructions on how to contribute your changes back to the project.

.. _hacking-antidote-web:

Hacking on Antidote-web
-----------------------

`Antidote-Web <https://github.com/nre-learning/antidote-web>`_ is Antidote's front-end. It is currently written in vanilla Javascript (no framework)
as well as the expected HTML/CSS stuff. It's also currently packaged with parts of the Apache guacamole
project, which is why you'll see it commonly deployed on Tomcat. This is something we're working on breaking
up a bit later.

To preview changes to Antidote-web, the project repo has a Makefile that can be used to build a test Docker container
that runs your local copy of Antidote-web as a standalone entity, with some mock data. Once in the Antidote-web
repository, simply run:

.. CODE::

    make test

This may take a few minutes the first time, but eventually you'll have a few containers running in Docker:

.. CODE::

    ~$ docker ps                                                                                                                                                                                            [22:15:00]

    CONTAINER ID        IMAGE                       COMMAND                  CREATED             STATUS              PORTS                    NAMES
    b13bf8a3aa63        antidotelabs/antidote-web   "/opt/guacamole/bin/…"   2 seconds ago       Up 1 second         0.0.0.0:8080->8080/tcp   aweb
    c17a8dce40d2        guacamole/guacd             "/bin/sh -c '/usr/lo…"   2 seconds ago       Up 1 second         0.0.0.0:4822->4822/tcp   guacd
    6e825b629bc6        antidotelabs/utility        "/usr/sbin/sshd -D"      3 seconds ago       Up 2 seconds        0.0.0.0:2222->22/tcp     linux1

You'll be able to access the Web UI at `http://localhost:8080 <http://localhost:8080>`_ now. Re-run ``make test``
every time you wish to rebuild the environment to incorporate changes.

.. _hacking-syringe:

Hacking on Syringe
------------------

`Syringe <https://github.com/nre-learning/syringe>`_ is an application written in Go which provides orchestration for lesson resources on
Kubernetes, while providing an API for the web front-end to consume.

To build Syringe, you'll need to install the version of Go specified in `Syringe's Dockerfile <https://github.com/nre-learning/syringe/blob/master/Dockerfile#L1>`_.
Whatever version of Go is used there, is the currently/officially supported version.

Once done, enter the Syringe repository. There are a few things you can do here. To simply compile Syringe
binaries, including ``syrctl`` and all of the server-side binaries, run:

.. CODE::

    make

You can also execute Syringe's tests with:

.. CODE::

    make test

This is the same command executed by the CI pipeline, so this is a good way to know if your tests will
pass before actually pushing anything.

You can also build Syringe's docker container with:

.. CODE::

    make docker

This includes a ``docker push`` step, so if you want to push this image to your own repository
for testing, you'll need to edit the push target.
