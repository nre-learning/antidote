.. _toolbox-presentation:

Endpoint Presentations
======================

At this point, hopefully you understand how :ref:`Endpoints <endpoints>` provide a basis for creating an interactive
learning experience. However, there's no interactivity unless those Endpoints are made accessible somehow
to the learner. Enter Presentations.

You can specify a list of Presentations on an Endpoint to indicate how you want that Endpoint to be "presented" to the
learner. A simple example is shown below. In this case, we're offering a single Presentation for an Endpoint, that provides
SSH terminal access to that endpoint over port 22:

.. CODE:: yaml

  endpoints:
  - name: linux1
    image: antidotelabs/utility
    presentations:
    - name: cli
      port: 22
      type: ssh

As you can see, each Presentation in the list has three fields for you to specify:

- ``name`` - The name of the presentation. This can be whatever you want, as long as it's relatively short and
  unique for that endpoint.
- ``port`` - The port that Antidote should use to access the container for this Presentation.
- ``type`` - This controls the type of presentation being offered. Currently supported options are ``ssh`` and ``http``.
  Read on for more details on these options.

You can get creative with Presentations. First and foremost, you probably noticed that the ``presentations`` attribute is
plural form, and provided as a YAML list. This is because you can have multiple Presentations to the same Endpoint:

.. CODE:: yaml

  endpoints:
  - name: linux1
    image: antidotelabs/utility
    presentations:
    - name: cli1
      port: 22
      type: ssh
    - name: cli2
      port: 22
      type: ssh
    - name: web
      port: 80
      type: http

These will all be shown as individual tabs in the Antidote web front-end, and they will be disambiguated via their
Presentation name. For instance, the example above will result in tabs ``linux1-cli1``, ``linux1-cli2``, and ``linux1-web``.

Finally, in some cases you don't want **any** presentations. A common example of this is some kind of endpoint that you
need to access from another Endpoint via REST API. You want to provide a Presentation to the user to execute some kind of
tool or script, but the Endpoint offering the REST API merely needs to exist in the environment and respond to queries.

In this case, omitting the ``presentations`` field is totally fine, with one caveat. If no Presentation is specified,
then the ``additionalPorts`` field becomes a required field.

.. CODE:: yaml

  endpoints:
  - name: linux1
    image: antidotelabs/utility
    presentations:
    - name: cli
      port: 22
      type: ssh

  - name: restapi
    image: antidotelabs/restapi
    additionalPorts: [80]

Because the above Endpoint ``restapi`` didn't have any presentations, we needed to ensure at least one port
was provided in ``additionalPorts``. The learner can then access the ``linux1`` endpoint and use the tooling
in that Endpoint to access the REST API of ``restapi``.

.. _presentation-options:

Presentation Options
~~~~~~~~~~~~~~~~~~~~~

There are some implementation details for each of the available presentation types specified in the ``type``
field that you should be aware of.

SSH
  **Usage:** ``type: ssh``

    This one is pretty straightforward. A very common use case for interacting with Endpoints is to provide
    an interactive CLI (Command Line Interface) terminal in the Antidote front-end. This is accomplished by connecting directly
    to the Endpoint via SSH, and using that connection to provide the experience to the web. Under the hood,
    the front-end uses Guacamole's SSH tunneling capabilities.

    As long as your Endpoint is configured to listen on the port you specify in the Presentation for SSH
    connections with the username ``antidote`` and ``antidotepassword``, Antidote will take care of
    connecting it to the user on the front-end.

HTTP
  **Usage:** ``type: http``

    Not all content is best shown via the CLI. Sometimes you want to be able to show some kind of web-based
    portal that's running on an Endopint, such as a self-service application, which interacts with other
    Endpoints on the back-end.

    In this case, the ``http`` type can be used. A tab will be opened for this Presentation, but instead of a
    terminal, the tab contents will show the web application you provide in the Endpoint (in an iframe). A few considerations
    for this option:

    - HTTPS is not currently supported. We need to iron out a few wrinkles in the implementation first, and we'll
      support either protocol, very soon. For now, use HTTP, and the Antidote load balancer will serve the content
      from a reverse proxy that provides HTTPS.
    - The web application must serve its content at a specific application root, which is provided to the Endpoint
      via an environment variable, ``SYRINGE_FULL_REF``. Make sure that your web server is configured to use that
      value as the application root.

VNC
  Not currently supported - `coming soon <https://github.com/nre-learning/antidote-web/issues/65>`_!

  When this is implemented, it will use Guacamole's Web VNC client to
  provide access, in the tab, to a graphical connection to a desktop
  displaying GUI applications running on the Endpoint.
