.. _syringe-config:

Configuring Syringe
================================

Syringe is configured through environment variables. Since Syringe is typically deployed on Kubernetes, the best
way to pass these to Syringe is directly in the ``Pod`` or ``Deployment`` definition:

.. code:: yaml

    (...truncated...)

    containers:
    - name: syringe
      image: antidotelabs/syringe:latest
      imagePullPolicy: Always
      env:
      - name: SYRINGE_CURRICULUM
        value: "/antidote"
      - name: SYRINGE_DOMAIN
        value: "localhost"

    (...truncated...)

If you're using `antidote-selfmedicate <https://github.com/nre-learning/antidote-selfmedicate>`_ to spin up an instance of Antidote and Syringe yourself, note that these are provided
in the included `Kubernetes manifest <https://github.com/nre-learning/antidote-selfmedicate/blob/master/syringe.yml>`_.

See the tables below for a description of each, as well as information on which are required, and which have default values.

Required
--------

.. list-table::
   :header-rows: 1

   * - Variable Name
     - Description
   * - SYRINGE_CURRICULUM
     - Directory where the curriculum is stored
   * - SYRINGE_DOMAIN
     - Domain where Antidote-web is running. Used to control ingress routing

Optional
--------

.. list-table::
   :width: 30
   :widths: 5 5 70
   :header-rows: 1

   * - Variable Name
     - Default Value
     - Description
   * - SYRINGE_GRPC_PORT
     - 50099
     - Port to use for Syringe's GRPC service
   * - SYRINGE_HTTP_PORT
     - 8086
     - Port to use for the grpc-gateway REST API for Syringe
   * - SYRINGE_TIER
     - local
     - Controls which lessons Syringe makes available based on lesson metadata. Can be ``local``, ``ptr``, or ``prod``.
   * - SYRINGE_CURRICULUM_LOCAL
     - false
     - Specify if the curriculum should be pulled from the local filesystem, bypassing the need to clone a repository.
   * - SYRINGE_CURRICULUM_VERSION
     - latest
     - The version of the curriculum to use. Primarily used for selecting the right tag for curriculum images.
   * - SYRINGE_LESSON_REPO_REMOTE
     - https://github.com/nre-learning/nrelabs-curriculum.git
     - Git repo from which to clone lessons into lesson endpoint pods
   * - SYRINGE_LESSON_REPO_BRANCH
     - master
     - Git branch to use in lesson endpoint pods
   * - SYRINGE_LIVELESSON_TTL
     - 30
     - The length of time (in minutes) a lesson is allowed to remain active before it is shut down.
   * - SYRINGE_INFLUXDB_URL
     - https://influxdb.networkreliability.engineering/
     - The URL for the influxdb metrics server
   * - SYRINGE_INFLUXDB_USERNAME
     - admin
     - The username for the influxdb metrics server
   * - SYRINGE_INFLUXDB_PASSWORD
     - zerocool
     - The password for the influxdb metrics server
   * - SYRINGE_ALLOW_EGRESS
     - false
     - Destination directory to use when cloning into lesson endpoint pods
   * - SYRINGE_PRIVILEGED_IMAGES
     - antidotelabs/container-vqfx,antidotelabs/vqfx-snap1,antidotelabs/vqfx-snap2,antidotelabs/vqfx-snap3,antidotelabs/vqfx-full,antidotelabs/cvx
     - Comma-separated array that specifies which images need privileged access granted to them at runtime