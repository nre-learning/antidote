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
with so they're not spinning your wheels, wondering what to do with a lesson.

Snippets and Jupyter notebooks

Adjust antidote-web to link here once this is done.


Writing Lab Guides with Markdown
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Many of these guides are written in Markdown, and then rendered as HTML into
the front-end as a readable guide. While these can contain code snippets that can
be automatically executed, it may be useful to embed interactive code right in the
lab guide.
For instance, you may want to execute some code in the left-hand pane where the lab
guide
is located, while looking at the output of a network device or other entity.

Writing Lab Guides with Jupyter Notebooks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. NOTE::

    This section is focused on lesson authors looking to use Jupyter notebooks in the creation of a lesson.
    If you're looking for an overview of how to **use** lesson guides in Antidote or NRE Labs, go
    :ref:`here <using-jupyter>`.

Write notebooks on your own, probably. The only difference should be DNS.

Lots of folks already have Jupyter notebooks and that's why this feature exists.. If you don't, you may want to consider writing your lesson guides in markdown.
Jupyter notebooks do add a layer of complexity if you are starting from scratch, so if you're going to be creating new content anyways,
you may as well write it in simple Markdown and use code snippets. However, if you already have notebooks that could be useful as lesson guides,
read on, because this feature exists for you.

Focused just on Python for now.