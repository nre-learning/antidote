.. _contrib-platform-docs:

Contributing to this Documentation
==================================

This documentation is powered by Sphinx and hosted by ReadTheDocs. The source for this documentation
is written in `reStructuredText (RST) <http://docutils.sourceforge.net/rst.html>`_,
and is located in the `"docs" directory of the Antidote repo <https://github.com/nre-learning/antidote/tree/master/docs>`_. 
Before contributing to the documentation, it's worth bookmarking the
`RST cheatsheet <http://docutils.sourceforge.net/docs/user/rst/quickref.html>`_ for future reference.
RST is fairly straightforward to use, and there's plenty of existing examples in these docs for you to reference,
but it's not without it's peculiarities, so keep that handy.

First-Time Setup
~~~~~~~~~~~~~~~~

To contribute to the docs, the first thing you'll want to do is fork and clone the
`Antidote repo <https://github.com/nre-learning/antidote>`_ so that a copy of the repo is hosted under your
username. Follow the :ref:`Antidote Git instructions <antidote-git>` to do this.

Once properly cloned, ``cd`` into the local repo's  ``docs`` directory:

.. CODE::

    cd antidote/docs/

Before continuing, you need to make sure you have a working Python installation, complete with the ``pip`` installation
utility. ``pip`` is available in most package managers (for instance, Ubuntu uses the package name ``python-pip``),
so if you don't have it, a quick Google search will set you straight.

Next, install the ``virtualenv`` package:

.. CODE::

    sudo pip install virtualenv

That should be the only thing we need root permissions for - now that we have ``virtualenv`` we can create a virtual
Python environment in the docs directory for everything else we need. Next, run the following commands to instantiate
this virtual environment, activate it, and install all of the dependencies needed to build the docs:

.. CODE::

    virtualenv venv
    source venv/bin/activate
    pip install -r requirements.txt

As long as you see the ``(venv)`` in your terminal prompt, you're "in" the virtual environment. If for any reason you have
to close your terminal or restart your computer, you can "re-enter" this environment by navigating to the same directory
and re-running ``source venv/bin/activate``.

If you got to this point, you shouldn't have to do this again. Building the docs now is a one-liner command, which
we'll cover in the next section.

Building the Docs
~~~~~~~~~~~~~~~~~

After the setup in the previous section, we're finally ready to build the documentation so that we have a local copy that's
been rendered from raw RST into a nice-looking HTML layout that's precisely like the online version.

This is accomplished with the simple command:

.. CODE::

    make clean html

This creates a directory ``_build/html``, and renders all of the raw RST source material into the HTML version you're
accustomed to seeing online. However, in this case, this is all done locally, so you can preview any changes you've made
immediately, by navigating to the file location within your browser:

.. CODE::

    file:///path/to/antidote/docs/_build/html/index.html

Once there you can click around and take a look at the result of your changes. You can keep this tab open and continue to make
changes to the RST source - when you want to again preview those changes, re-run ``make clean html`` and refresh the page.

Pushing your Changes
~~~~~~~~~~~~~~~~~~~~

Once you've iterated a few times on your docs changes, and you're happy with the preview results, you can follow
the :ref:`Antidote Git instructions <antidote-git>` to commit your changes, push them, and open a pull request.
