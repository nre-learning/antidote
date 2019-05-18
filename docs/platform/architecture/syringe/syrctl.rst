.. _syrctl:

The Syringe Client - ``syrctl``
===============================

While Syringe itself is primarily thought of as the orchestrator that sits behind the scenes within
Antidote, that's not all it can do. For each release of Syringe, a totally separate binary is compiled,
called ``syrctl``. This is the command-line cline for Syringe, and while a popular use case for this
is to control the back-end Syringe component(s), there are plenty of things that ``syrctl`` can do
all on its own.

.. _download-syrctl:

Download ``syrctl``
^^^^^^^^^^^^^^^^^^^

For every release of the Antidote platform, a corresponding release is created for Syringe. You can
`always find the latest release here <https://github.com/nre-learning/syringe/releases/latest>`_, where
precompiled binaries of Syringe have been posted. Download the file appropriate for your system, and extract
the binaries into a directory on your ``$PATH`` (or extract them anywhere and run via relative path). Either is fine.

.. _syrctl-validate:

Validating Lesson Content
^^^^^^^^^^^^^^^^^^^^^^^^^

One of the things ``syrctl`` can do for us is validate lesson content to make sure it has all of the basics to work properly. This is done via the subcommand
``syrctl validate``. This command is directed at a curriculum directory in order to work: for instance, we have the NRE Labs curriculum installed locally:

.. code::

    ~$ ls -lha
    total 68K
    drwxr-xr-x  6 mierdin mierdin 4.0K Apr 21 22:52 .
    drwxr-xr-x 10 mierdin mierdin 4.0K Apr 15 23:19 ..
    drwxrwxr-x  3 mierdin mierdin 4.0K Apr 17 17:39 collections
    drwxr-xr-x  8 mierdin mierdin 4.0K Apr 23 21:27 .git
    drwxr-xr-x 18 mierdin mierdin 4.0K Apr  6 12:49 images
    drwxr-xr-x  5 mierdin mierdin 4.0K Apr 21 22:52 lessons
    -rw-r--r--  1 mierdin mierdin 5.2K Apr 21 22:54 CHANGELOG.md
    -rwxr-xr-x  1 mierdin mierdin  500 Apr 15 15:19 check-changelog.sh
    -rw-rw-r--  1 mierdin mierdin    0 Apr 21 13:04 curriculum.meta.yaml
    -rw-r--r--  1 mierdin mierdin   33 Apr  6 12:49 .dockerignore
    -rw-r--r--  1 mierdin mierdin  573 Apr  6 12:49 .gitignore
    -rw-r--r--  1 mierdin mierdin  12K Apr  6 12:49 LICENSE
    -rw-r--r--  1 mierdin mierdin 1.1K Apr 15 18:56 README.md
    -rw-r--r--  1 mierdin mierdin  288 Apr  6 12:49 .travis.yml
    -rwxr-xr-x  1 mierdin mierdin  288 Apr 15 15:19 validate-lessons.share

We're already `cd`'d into this directory, so we just need to run ``syrctl validate .`` to instruct syrctl to validate the local directory:

.. code::

    ~$ syrctl validate .
    INFO[0000] Successfully imported lesson 14: Introduction to YAML --- BLACKBOX: 0, IFR: 0, UTILITY: 1, DEVICE: 0, CONNECTIONS: 0 
    INFO[0000] Successfully imported lesson 16: Using Jinja for Configuration Templates --- BLACKBOX: 0, IFR: 0, UTILITY: 1, DEVICE: 0, CONNECTIONS: 0 
    INFO[0000] Successfully imported lesson 17: Version Control with Git --- BLACKBOX: 0, IFR: 0, UTILITY: 1, DEVICE: 0, CONNECTIONS: 0 
    INFO[0000] Successfully imported lesson 19: Working with REST APIs --- BLACKBOX: 0, IFR: 0, UTILITY: 1, DEVICE: 3, CONNECTIONS: 4 
    INFO[0000] Successfully imported lesson 22: Introduction to Python --- BLACKBOX: 0, IFR: 0, UTILITY: 1, DEVICE: 0, CONNECTIONS: 0 
    INFO[0000] Successfully imported lesson 23: Linux Basics --- BLACKBOX: 0, IFR: 0, UTILITY: 1, DEVICE: 0, CONNECTIONS: 0 
    INFO[0000] Successfully imported lesson 12: Network Unit Testing with JSNAPY --- BLACKBOX: 0, IFR: 0, UTILITY: 1, DEVICE: 3, CONNECTIONS: 3 
    INFO[0000] Successfully imported lesson 13: Multi-Vendor Network Automation with NAPALM --- BLACKBOX: 0, IFR: 0, UTILITY: 1, DEVICE: 1, CONNECTIONS: 0 
    INFO[0000] Successfully imported lesson 15: Event-Driven Network Automation with StackStorm --- BLACKBOX: 0, IFR: 0, UTILITY: 1, DEVICE: 3, CONNECTIONS: 3 
    INFO[0000] Successfully imported lesson 18: End-to-End Network Testing with ToDD --- BLACKBOX: 0, IFR: 0, UTILITY: 2, DEVICE: 1, CONNECTIONS: 2 
    INFO[0000] Successfully imported lesson 24: Junos Automation with PyEZ --- BLACKBOX: 0, IFR: 0, UTILITY: 1, DEVICE: 1, CONNECTIONS: 1 
    INFO[0000] Successfully imported lesson 25: Juniper Extension Toolkit (JET) --- BLACKBOX: 0, IFR: 0, UTILITY: 1, DEVICE: 1, CONNECTIONS: 1 
    INFO[0000] Successfully imported lesson 26: Vendor-Neutral Network Configuration with OpenConfig --- BLACKBOX: 0, IFR: 0, UTILITY: 1, DEVICE: 1, CONNECTIONS: 1 
    INFO[0000] Successfully imported lesson 29: Using Robot Framework for Automated Testing --- BLACKBOX: 0, IFR: 0, UTILITY: 1, DEVICE: 1, CONNECTIONS: 1 
    INFO[0000] Successfully imported lesson 30: Network Automation with Salt --- BLACKBOX: 0, IFR: 0, UTILITY: 1, DEVICE: 1, CONNECTIONS: 1 
    INFO[0000] Successfully imported lesson 31: Terraform & Junos --- BLACKBOX: 0, IFR: 0, UTILITY: 1, DEVICE: 3, CONNECTIONS: 3 
    INFO[0000] Successfully imported lesson 21: Automating the Troubleshooting Chain --- BLACKBOX: 2, IFR: 0, UTILITY: 2, DEVICE: 3, CONNECTIONS: 6 
    INFO[0000] Successfully imported lesson 32: Automated STIG Compliance Validation --- BLACKBOX: 0, IFR: 0, UTILITY: 1, DEVICE: 1, CONNECTIONS: 0 
    INFO[0000] Successfully imported lesson 33: Quick and Easy Device Inventory --- BLACKBOX: 0, IFR: 0, UTILITY: 1, DEVICE: 2, CONNECTIONS: 0 
    INFO[0000] Successfully imported lesson 34: Automated Device Configuration Backup --- BLACKBOX: 0, IFR: 0, UTILITY: 1, DEVICE: 2, CONNECTIONS: 0 
    INFO[0000] Successfully imported lesson 35: Device Specific Template Generation --- BLACKBOX: 0, IFR: 0, UTILITY: 1, DEVICE: 2, CONNECTIONS: 0 
    INFO[0000] Imported 21 lesson definitions.              
    All detected lesson files imported successfully.

This runs the exact same logic that ``syringed`` would use to load lessons on the server-side, so this is a really handy way to make sure the basics
of curriculum definitions are done correctly.

On the `NRE Labs Curriculum repository <https://github.com/nre-learning/nrelabs-curriculum>`_, we're actually running ``syrctl validate`` on every new
Pull Request to ensure things are set up properly, as much as possible.


There are things it won't check - like the validity of a network configuration, or that your Docker image
is built properly, but in terms of the things that Syringe requires, it will give you confidence in
a stable starting point, rather than reading through a list of points in this doc.

Automatic Lesson Creation
^^^^^^^^^^^^^^^^^^^^^^^^^

This is TBD. In the future, ``syrctl`` will contain a command for bootstrapping a new lesson more easily.

