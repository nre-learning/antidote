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

``syrctl validate``
^^^^^^^^^^^^^^^^^^^

Some of the capabilities of the Antidote platform are overviewed elsewhere in this documentation.
However, often, people run into the problem of creating lessons, and uploading them to a branch, only
to find out that they're missing a configuration, or a stanza in their lesson definition.

For these stricter requirements, rather than document them, we've built all these rules into the
``syrctl validate`` subcommand. This command will execute on a curriculum, and will raise warnings
or errors based on problems. If this command runs without errors, you should have the basics covered.

There are things it won't check - like the validity of a network configuration, or that your Docker image
is built properly, but in terms of the things that Syringe requires, it will give you confidence in
a stable starting point, rather than reading through a list of points in this doc.

``syrctl lesson create``
^^^^^^^^^^^^^^^^^^^^^^^^

TBD - this doesn't exist yet, but the idea is that we will provide an interactive wizard for creating a
new lesson from scratch. For now, look at existing lesson content, and modify to suit your needs.

