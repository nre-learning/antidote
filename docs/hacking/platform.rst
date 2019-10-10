.. _hacking-platform:

Hacking on the Antidote Platform
================================

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

`Antidote-Web <https://github.com/nre-learning/antidote-web>`_ is Antidote's front-end. It is currently
written in vanilla Javascript (no framework) as well as the expected HTML/CSS stuff. It's also currently
packaged with parts of the Apache guacamole project, which is why you'll see it commonly deployed on Tomcat.
This is something we're working on breaking up a bit later.

There are three main subcomponents to Antidote-web:

- The actual in-browser application code (javascript)
- A minimal Java servlet to handle tunnel requests from the front-end Guacamole library
- A daemon (guacd) that proxies tunnel requests to the actual endpoint Guacamole wants to connect to

For now, the top two are deployed together on top of Tomcat, though in the future we may split this up.

In addition to the components listed above, when doing development on Antidote-web, it's incredibly useful to
have a working instance of Syringe, since the Syringe API is where Antidote-web gets all its information. It is
also useful to have actual SSH or HTTP endpoints to connect to in the web UI, so you can see how those things work.

In the Antidote-web repo, a Makefile is provided which stands up a bare-minimum set of containers to allow you
to build and run the Antidote-web application from your own local source code. First, ensure the following is
installed properly on your machine, as the Makefile depends on it:

- Docker
- Docker Compose

Next, clone and ``cd`` to the `Antidote-Web <https://github.com/nre-learning/antidote-web>`_ repository, and run:

.. CODE::

    make hack

This may take a few minutes the first time. Once you see a log message on the console that says something like
``org.apache.catalina.startup.Catalina.start Server startup in...``, you will be able to access the Web UI at
`http://localhost:8080 <http://localhost:8080>`_.

To rebuild the environment, break out with ``Ctrl+c``, and re-run ``make hack``.

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
