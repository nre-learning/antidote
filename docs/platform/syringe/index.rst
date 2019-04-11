.. _syringe:

Syringe - Antidote's "Brains"
================================

.. toctree::
   :maxdepth: 1

   configuration.rst
   syrctl.rst

Syringe is where the real work gets done in the Antidote project. It's responsible for taking in lesson definitions
via :ref:`a YAML file <lessons>`, and any configs, scripts, etc used in the lesson, and providing them to the
front-end via its API.

Syringe is primarily configured through :ref:`environment variables <syringe-config>`.