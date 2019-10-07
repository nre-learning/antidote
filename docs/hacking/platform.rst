.. _hacking-platform:

Hacking on the Antidote Platform
================================

There are two main components to the Antidote platform:

- Antidote-web
- Syringe

In this document, we'll explain what it takes to work on the code.

.. _hacking-antidote-web:

Hacking on Antidote-web
-----------------------

.. NOTE::

    This section discusses technical steps for building Antidote-web yourself when working on the code. See
    :ref:`here <contrib-platform>` for instructions on how to contribute your changes back to the project.

Antidote-web is a Web application mainly coded in Javascript coupled to
elements of the Apache Guacamole project.
         
Detailed instructions are WIP - coming soon! In the meantime, just know there is a Makefile in this repository
and you can run ``make`` to rebuild the Docker container for `antidote-web`.

.. _hacking-syringe:

Hacking on Syringe
------------------

.. NOTE::

    This section discusses technical steps for building Syringe yourself when working on the code. See
    :ref:`here <contrib-platform>` for instructions on how to contribute your changes back to the project.

Syringe is mainly an application written in Go which provides orchestration for lesson resources on Kubernetes, while providing an API for the web front-end to consume.
         
Detailed instructions are WIP - coming soon! In the meantime, just know there is a Makefile in this repository
and you can run ``make docker`` to rebuild the Docker container for Syringe, or simply ``make`` to compile from
source. You can also run ``make test`` to run the unit tests for the project.
