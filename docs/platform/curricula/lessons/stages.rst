Stages
======

When learning any topic, it's important to be able to break it up into reasonable "chunks". No one wants to start at a wall
of learning material they know will take them the better part of an afternoon to get through.

In Antidote, lessons are broken up into Stages. We'll also use the term "Labs" to describe these from time-to-time; consider them
synonomous. The intention behind Stages is to provide a logical place to "break up" lesson content. You can think of them like
chapters in a textbook; where the goal of an Algebra textbook is to teach algebra, we really only care about linear equations in
Chapter 1. Those not only provided bounded structures for learning, where the learner is able to more easily wrap their head around
the content and feel like they've accomplished something, it also helps them understand the path in front of them.

In any lesson, Stages are defined using the `stages` stanza in the lesson definition file:

.. CODE:: yaml

    stages:
    - id: 1
      description: No BGP config - tests fail

    - id: 2
      description: Correct BGP config - tests pass

When a lesson is loaded in the web front-end, it shows up as a dropdown at the top of the page:

.. image:: /images/labs.png
   :align: center

While the Stage definition seems simple, there's a lot that goes on when a user navigates between Stages by selecting
something in that drop-down:

- All Endpoints with a `configurationType` :ref:`configured <toolbox-config>` will be reconfigured accordingly. This happens
  when a lesson is initially loaded
- Endpoint health checks as described in :ref:`Endpoint Presentations <toolbox-presentation>` are **not** done between stages.
  Presentations are static for the whole lesson, regardless of Stage. They're done when the lesson is initially loaded
- When a stage ID is omitted, the default is to load the first one, but this isn't a requirement for users. Each lesson URL
  includes a Stage ID, which means hyperlinks to any stage in any lesson are honored. What this means for lesson builders is
  that while your Stages can (and should) have a natural progression, you should not rely on users to have done something themselves
  in Stage 1 in order for Stage 2 to work. If you have the user accomplish a task in Stage 2, you should still overwrite all configs
  yourself to the expected value in Stage 2's configurations.

Each Stage has a particular directory structure that you should be aware of. As with most things involving curriculum resource definition,
most of this is enforced by ``syrctl`` so you can validate this structure yourself, but here are some general rules:

.. CODE::

    .
    ├── jsnapy_config.yaml
    ├── jsnapy_tests.yaml
    ├── lessondiagram.png
    ├── lesson.meta.yaml
    ├── stage1
    │   ├── configs
    │   │   ├── vqfx1.txt
    │   │   ├── vqfx2.txt
    │   │   └── vqfx3.txt
    │   └── guide.md
    └── stage2
        ├── configs
        │   ├── vqfx1.txt
        │   ├── vqfx2.txt
        │   └── vqfx3.txt
        └── guide.md

- Each stage must have a corresponding directory called ``stage<N>`` where ``N`` is the stage ID.
- Each stage directory must have a ``configs`` directory, where all of the files related to :ref:`Endpoint configuration <toolbox-config>`
  should be kept.
- Each stage directory must also have either a markdown-based lesson guide, or a jupyter notebook to be used for the same. We'll get into
  the differences between these in the next few sections.

Lab Guides
----------

All NRE Labs lessons come with lab guides. These are meant to be something the learner can follow along
with so they're not spinning your wheels, wondering what to do with a lesson. It is also meant to include snippets of code or
commands for them to execute, or have executed for them. There are two options for lesson guides in Antidote today:

- Markdown
- Jupyter Notebooks

You can choose either of these options **on a per-stage basis**. This means that Stage 1 can have a Markdown lesson guide,
Stage 2 a Jupyter notebook, and Stage 3 back to Markdown, if you want. The
`NRE Labs NAPALM lesson <https://labs.networkreliability.engineering/labs/?lessonId=13&lessonStage=1>`_ is a good example of a lesson
that leverages both options. The sections below will explain how to use either option.

Writing Lab Guides with Markdown
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The simplest option by far is to write lab guides with `Markdown <https://daringfireball.net/projects/markdown/syntax>`_. This is an
extremely popular, simple formatting syntax for creating rich documents from plain-text sources. Most of the time when you see a
``README`` file on a Github repository, the chances are very good that it's written in Markdown. What Github does is translate the raw text
of the file into richly formatted, rendered versions appropriate for viewing in a web browser.

To enable this same experience for Antidote, lesson guides can be written in Markdown, and ``antidote-web`` will take care of translating
the source file into HTML to be presented to the user. This means you can use anything available to you in the
`Markdown <https://daringfireball.net/projects/markdown/syntax>`_.

.. NOTE::

  You don't have to use selfmedicate to preview the HTML version for your Markdown documents. While every
  Markdown renderer is a bit different, and there might be some minor differences within the Antidote front-end,
  if you're just looking for some basic HTML preview functionality, there are plenty of tools to do this:

  - Keeping in the spirit of doing everything in the browser, `Dillinger <https://dillinger.io/>`_ is **very handy** for
    working on lesson guides with a constant preview.
  - Most popular text editors also have markdown preview functionality built in or available via plugin. For example,
    there's good support for this in `VS Code <https://code.visualstudio.com/docs/languages/markdown>`_
  - There are a number of CLI tools available as well for doing the conversion yourself, such as `Pandoc <https://pandoc.org/>`_,
    if you are so inclined.

While native Markdown is perfectly fine, there's one feature built into ``antidote-web`` you should be aware of that really uplevels
your lesson guide. In Markdown, you can wrap a bit of text with triple-backticks, and it will preserve the formatting you use within that block.
This is very useful for code or CLI commands, where the structure is very important.

.. CODE::

    ```
    echo "Hello, World!"
    ```

Markdown-based lab guides include the ability to add a "Run this snippet" button to automatically
run the contents of a code snippet in a given terminal tab. To do this, the lesson author only needs
to add some HTML underneath each snippet:

.. code::

    ```
    echo "Hello, World!"
    ```
    <button type="button" class="btn btn-primary btn-sm" onclick="runSnippetInTab('linux1', this)">Run this snippet</button>

Most of the HTML shown above can remain the same, but in the above example ``linux1`` refers to the endpoint where this snippet should be
executed. The front-end will switch to the tab named accordingly and paste that text automatically. So, you'll need to edit this
to point to the tab you want.

Also, when you're adding a snippet to a lesson guide, sometimes you may want an extra newline run at the end.
For example, if you are executing some Python code, and your snippet ends on a loop, or a conditional,
you need an extra newline to get the interpreter to understand you're done defining the loop.

The solution to this is to use ``<pre>`` tags in lieu of the traditional triple-backtick for embedding
code in Markdown. For instance, instead of this:

.. code::

    ```
        (code)
    ```

Do this:

.. code::

    <pre>
        (code)
    </pre>

These are rendered exactly the same way in the lesson guide, but the latter is interpreted much more literally
when being pasted into the terminal window, meaning the extra newline is executed like any other character.

Finally, when you have a lesson guide ready. place it in the stage directory as ``guide.md``. This is where the Antidote platform will
look for this lesson guide.

Writing Lab Guides with Jupyter Notebooks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. NOTE::

    This section is focused on lesson authors looking to use Jupyter notebooks in the creation of a lesson.
    If you're looking for an overview of how to **use** lesson guides in Antidote or NRE Labs, go
    :ref:`here <using-jupyter>`.

Many folks who have invested time in education on automation or related topics have some experience with `Jupyter notebooks <https://jupyter.org/>`_.
First of all, Jupyter is awesome, and second, it's not fair to force folks to convert that content to Markdown just to get it working with Antidote.
So, Antidote natively supports the use of Jupyter notebooks as lab guides in lieu of a Markdown-based guide.

.. WARNING::

  Fair warning - Jupyter notebooks offer a lot more functionality than Markdown-based lab guides, but they do add a layer of complexity as a result.
  So, if you're starting from scratch, it's *probably* best to start with Markdown-based lab guides. However, the choice is yours.

Even cooler - any lesson that uses a Jupyter notebook is automatically provisioned a background Endpoint dedicated to running that notebook,
that is run alongside all other Endpoints for that lesson. That means that you can take advantage of Kubernetes DNS when referring to other
Endpoints in your notebooks. If you want to send a REST API request to an Endpoint with the name of ``webapp``, you can refer to it via the hostname
``webapp``, right in the notebook. No need to figure out IP addresses for stuff.

To use a Jupyter notebook as a lesson guide in an Antidote lesson, you need only add the line ``jupyterLabGuide: true`` to each Stage that
requires it in your lesson definition. Here's an example of a lesson that uses Jupyter notebooks for stages 1, 2, and 4, but uses the traditional
Markdown format for stage 3:

.. CODE:: yaml

  stages:
    - id: 1
      description: Get device facts
      jupyterLabGuide: true
    - id: 2
      description: Get information with NAPALM "getter" functions
      jupyterLabGuide: true
    - id: 3
      description: The NAPALM Command-Line Utility
    - id: 4
      description: Make configuration changes with NAPALM
      jupyterLabGuide: true

When you do this, you will need to make sure that a jupyter notebook titled ``notebook.ipynb`` is in all relevant stage directories.
This obviates the need for a ``guide.md` file.

If you're starting from scratch and wish to write a Jupyter notebook, your best bet is to follow an
`online Jupyter notebook tutorial <https://www.codecademy.com/articles/how-to-use-jupyter-notebooks>`_ to get it started. Or you can
copy one from an existing lesson into your lesson, and once spun up, you can use the Jupyter GUI to edit and download the revised notebook.
