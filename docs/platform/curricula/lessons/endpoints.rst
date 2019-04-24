.. _toolbox-endpoints:

Lesson Endpoints
============================

"Endpoint" is the generic term used in the Antidote project to describe the various pieces of software
you'll need to use in a given lesson in order to teach a particular subject. This include virtual routers
and switches, of course, but they can also include simple linux containers to run a script.

Within the context of the Antidote platform, there are a few types of Endpoints that you, the
lesson author should be aware of. Knowing the intention behind, and the capabilities of, each endpoint
type, is crucial to being able to

.. WARNING::

    While these endpoint types are mostly thought to be fairly stable, how they're configured within a lesson
    definition is subject to change. Please revisit this page, and the :ref:`lesson definition <lessons>`
    page for the most up-to-date information possible.

The concept of an "Endpoint" is an abstraction within the Antidote infrastructure, but the actual runtime
for making endpoints real is Kubernetes. This is why Syringe communicates directly with the Kubernetes
API for instantiating containers. Endpoints are really just containers being executed in Kubernetes
in various ways. As a result, you'll often see the ``image`` field in an endpoint definition. This is
literally a docker image, such as a full docker hub repository, like ``antidotelabs/vqfx``.

Generally, endpoints are configured within the main :ref:`lesson definition <lessons>` file, ``syringe.yaml``,
which can be found at the root of any lesson directory. Declaring these endpoints in a lesson definition is
usually very simple - often only a name and a reference to the docker hub image is needed. However,
the way that Syringe will handle the endpoint will differ greatly between the various endpoint types.

Currently, there are three endpoint types:

* Utility
* Device
* Blackbox

Each endpoint type is handled differently with respect to how it is accessed, how it's determined to be
healty, and if applicable, how it's automatically configured during a lesson. All of this will be defined
below.

Utility
^^^^^^^

The ``utility`` is the simplest way to present something to the user in Antidote. An endpoint
of this type will be presented in the web front-end as a terminal tab. As a result, the endpoint
must be accessible via SSH. See the table below for details.

A sample configuration (found in a :ref:`lesson definition <lessons>`) is below:

.. CODE:: yaml

  utilities:
  - name: linux1
    image: antidotelabs/utility

+----------------------+---------------------------------------------------+
|  Endpoint Attribute  |            Detail                                 |
+======================+===================================================+
| Health Check         |  SSH-based. Endpoints must be reachable via port  |
|                      |  22, and authenticate with                        |
|                      |  antidote/antidotepassword                        |
+----------------------+---------------------------------------------------+
| Autoconfiguration    |  No autoconfiguration (yet)                       |
+----------------------+---------------------------------------------------+
| Default Ports        |  Port 22 is opened by default. Lesson authors can |
|                      |  specify additional ports.                        |
+----------------------+---------------------------------------------------+

Device
^^^^^^

The ``device`` endpoint type is ideal for running network devices like routers and switches. It's
very similar to the ``utility`` type, with one major difference - how it's automatically
configured (see table below). It also requires SSH connectivity and has the same default port
configuration as a ``utility``. It is also represented as a terminal tab in the web UI.

A sample configuration (found in a :ref:`lesson definition <lessons>`) is below:

.. CODE:: yaml

  devices:
  - name: vqfx1
    image: antidotelabs/vqfx:snap1
  - name: vqfx2
    image: antidotelabs/vqfx:snap2
  - name: vqfx3
    image: antidotelabs/vqfx:snap3

+----------------------+---------------------------------------------------+
|  Endpoint Attribute  |            Detail                                 |
+======================+===================================================+
| Health Check         |  SSH-based. Endpoints must be reachable via port  |
|                      |  22, and authenticate with                        |
|                      |  antidote/antidotepassword                        |
+----------------------+---------------------------------------------------+
| Autoconfiguration    |  :ref:`Autoconfiguration <toolbox-autoconfig>`    |
|                      |  is done via NAPALM.                              |
+----------------------+---------------------------------------------------+
| Default Ports        |  Port 22 is opened by default. Lesson authors can |
|                      |  specify additional ports.                        |
+----------------------+---------------------------------------------------+

Blackbox
^^^^^^^^

Often, lesson authors need a piece of software running within a lesson environment, but don't
need (or even want) it to be shown to the user. For instance, you may have a ``utility`` endpoint
where the learner can execute a Python script to call some kind of API, but you need
another endpoint that actually serves up that API. You only need the first endpoint to show anything
to the user, but you need both running in parallel.

The ``blackbox`` type is ideal for this. It allows you to define an endpoint that is instantiated in the
lesson environment like any other endpoint, but no presentation to the learner is made.

Since it's not clear how you might want to access this endpoint, no default ports are provided, and
healthchecks are TCP-based, instead of full SSH-authentication checks (see table below).

A sample configuration (found in a :ref:`lesson definition <lessons>`) is below. In this example,
a ``blackbox`` endpoint that runs an IP PBX is configured alongside a ``utility`` image that runs
a soft phone client that the learner uses to register to the PBX:

.. CODE:: yaml

  blackboxes:
  - name: asterisk
    image: antidotelabs/asterisk
    ports: [8088]
    
  utilities:
  - name: sipphone
    image: antidotelabs/pjsua-lindsey

+----------------------+-----------------------------------------------------+
|  Endpoint Attribute  |            Detail                                   |
+======================+=====================================================+
| Health Check         |  Basic TCP probes based on defined open ports       |
+----------------------+-----------------------------------------------------+
| Autoconfiguration    |  No autoconfiguration.                              |
+----------------------+-----------------------------------------------------+
| Default Ports        |  No default ports. Lesson authors must explicitly   |
|                      |  specify a list of ports to open. See example above |
+----------------------+-----------------------------------------------------+ 
