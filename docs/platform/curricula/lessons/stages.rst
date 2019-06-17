Stages
======

Explanation of the intention behind stages, and what happens when navigating between them.
How to configure them in a lesson definition, and the required directory structure.

Lab Guides
~~~~~~~~~~

All NRE Labs lessons come with lab guides. These are meant to be something the learner can follow along
with so they're not spinning your wheels, wondering what to do with a lesson.

Snippets and Jupyter notebooks

Adjust antidote-web to link here once this is done.


Markdown Lab Guides
~~~~~~~~~~~~~~~~~~~

Many of these guides are written in Markdown, and then rendered as HTML into
the front-end as a readable guide. While these can contain code snippets that can
be automatically executed, it may be useful to embed interactive code right in the
lab guide.
For instance, you may want to execute some code in the left-hand pane where the lab
guide
is located, while looking at the output of a network device or other entity.

Using Jupyter Notebook Lab Guides
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. NOTE::

    This section focuses on how to use Jupyter notebooks in a lesson. If you're a lesson author looking to use Jupyter notebooks
    in your lesson, we'll cover that in the next section.

Jupyter notebooks are a great tool for accomplishing this, as a lesson author is able to put executable code snippets
right alongside readable text explaining it. To facilitate their use, NRE Labs optionally allows lesson authors to specify a
jupyter notebook in lieu of a markdown file for use as a lab guide.

If you encounter a jupyter notebook within a lesson, you might be initially overwhelmed with the number of buttons
and options. Don't worry about that - you really only need to know a few key things.

.. image:: /images/jupyter.png

The above image shows the toolbar for a jupyter notebook. You'll find this immediately below the dropdown selector where you can
navigate between the labs within a lesson. The main thing you will use here is the "run" button. This is what allows you to
execute a selected snippet of code. For instance, in the below image, we have a python snippet embedded in the lab guide.
We've selected it, and can execute the code within using this "run" button:

.. image:: /images/jupyter_selected.png

Depending on the snippet, you might see some output below.

.. image:: /images/jupyter_output.png

Note that you might not get any output. This depends on whether or not the code being executed is meant to produce output,
and/or how long it takes to process the instruction.

Also note that most jupyter notebooks expect that you'll run all of the snippets in order.
Not doing this might result in some errors. Just follow the instructions in the lab guide if you get stuck.

Finally, you can edit the contents of a notebook! The text and code provided is just part of the lab, but the
great thing about jupyter notebooks is that you can play around with them, and download a modified version.

.. image:: /images/jupyter_edit.png

Play around with editing the code provided and running it again! Experiment and learn!


Writing Lab Guides using Jupyter Notebooks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Write notebooks on your own, probably. The only difference should be DNS.

Lots of folks already have Jupyter notebooks and that's why this feature exists.. If you don't, you may want to consider writing your lesson guides in markdown.
Jupyter notebooks do add a layer of complexity if you are starting from scratch, so if you're going to be creating new content anyways,
you may as well write it in simple Markdown and use code snippets. However, if you already have notebooks that could be useful as lesson guides,
read on, because this feature exists for you.

Focused just on Python for now.