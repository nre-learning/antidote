Endpoints
============================

A foundational concept within Antidote is the ability to run the software or appliances needed
to educate the learner about a particular topic. It's nice to have lesson guides that walk
through a concept, but the whole point of the Antidote project was to provide that ease of use
without sacrificing any of the interactivity that comes with being able to play with the tech directly.

Antidote offers the concept of "Endpoints" to accomplish this. At its core, an Endpoint is simply a
Docker container that is built to run some software. This could be a simple Bash/CLI environment,
it could be a web server, or even a full-blown network device. Bottom line, if you want the user
to interact with something in your lesson, you need Endpoints.

Generally, Endpoints are configured within the :ref:`lesson definition <lessons>` file, ``lesson.meta.yaml``,
which can be found at the root of any lesson directory. Within this file, Endpoints are declared under the
``endpoints`` key, like so:

.. CODE:: yaml

  endpoints:
  - name: linux1
    image: antidotelabs/utility
    presentations:
    - name: cli
      port: 22
      type: ssh

  - name: vqfx1
    image: antidotelabs/vqfx:snap1
    configurationType: napalm-junos
    presentations:
    - name: cli
      port: 22
      type: ssh
    additionalPorts: [830]

A few points about the above:

- The ``name`` field is up to you to define - you can call each endpoint whatever you want, provided all endpoints
  have a unique name.
- The ``image`` field is a DockerHub-compatible image reference, which is passed directly to the underlying Kubernetes
  infrastructure to run your image. :ref:`See here for more information on images <lessonimages>`.
- The ``configurationType`` field is optional, and allows you to specify what kind of automatic
  configuration should be done for this endpoint. :ref:`See here for more information on endpoint configuration <toolbox-config>`.
- The ``presentations`` field is also optional, and allows you to specify ways that this endpoint should be presented to
  the user. This could be a CLI terminal, or even a web application with it's own tab.
  :ref:`See here for more information on endpoint presentations <toolbox-presentation>`.
- The ``additionalPorts`` field allows you to specify any additional ports that should be opened for this endpoint.
  By default, only the ports listed in a ``presentation`` are opened. So, this field allows you to directly specify
  ports that should be opened regardless of the presentations that are configured.


Health Checks
~~~~~~~~~~~~~

In order to know if a lesson is running, Syringe will perform health checks on endpoints based on each endpoint's configured
``presentations`` field. By default, for every Presentation, Syringe will perform a basic TCP connection periodically
as a heartbeat to ensure that these presentations are accessible. This means that each endpoint must be able to provide connectivity
on every port opened by a Presentation.

Some endpoints may not have any Presentations - in this case, the ``additionalPorts`` field is required, and must have at least one port
configured. Syringe will then use the first port in this list to perform a health check, and will mark the endpoint as healthy.

Once all endpoints are viewed as healthy, based on these health checks, the lesson will move into the configuration stage, or if no configuration
is necessary, will move directly into the Ready state, so that the web front-end can start offering the content to the learner.

Endpoint Environment Variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Syringe, which performs back-end orchestration for the Antidote platform, maintains a significant amount of context for each lesson.
Sometimes, endpoints need to be made aware of some of this context in order to properly show their content. A good example of this is a webserver
that needs to offer it's content at a specific application root based on the way that HTTP-based presentations work.
In this case, the Endpoint running that webserver would need to know the appropriate path that Syringe is wiring up for it.

To convey this detail, as well as others, all Endpoint containers/pods will be started with some environment variables. They are listed below:

======================================  ============================================================
SYRINGE_FULL_REF                          The full reference for an Endpoint, which is lesson id plus session
                                          ID plus endpoint name. (e.g. ``31-51fd1922sq55loah-ns-vqfx3``)
======================================  ============================================================

