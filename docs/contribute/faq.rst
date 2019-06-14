.. _curriculum-tips:

Tips and FAQs
=============

Snippet Indices
~~~~~~~~~~~~~~~
Lesson Guides include the ability to add a "Run this snippet" button to automatically run the contents of a code snippet
in a given terminal tab. To do this, the lesson author needs to add some HTML underneath each snippet:

.. code::

    ```
    echo "Hello, World!"
    ```
    <button type="button" class="btn btn-primary btn-sm" onclick="runSnippetInTab('linux1', this)">Run this snippet</button>

It used to be true that you had to provide the 0-based index of the snippet in question. However, as of v0.4.0, you can use the keyword
`this` as in the above example.

The previous method is still possible, but this new method is highly preferred, so you don't have to bother counting the snippets
in a lesson guide when you create these buttons. Just position the HTML below the snippet in question and you're good.

Newlines at the end of snippets
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
When you're adding a snippet to a lesson guide, sometimes you may want an extra newline run at the end.
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

How can I stand up a development environment to test my curriculum contributions?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The :ref:`selfmedicate <selfmedicate>` documentation is exactly what you need. This
environment allows you to spin up a local instance of Antidote on your own machine, and map your
curriculum into it so you can see your changes live without having to open a pull request right away.

How are you running network devices in this thing?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Everything in Antidote is executed in Kubernetes, so everything has to be a container. On the surface, this
may seem like a barrier to being able to run virtual networking images, which are commonly available as
virtual machines. Indeed, a common misconception is that the two models are mutually exclusive, but
they're not.

At the end of the day, a container is just a highly configured process, and QEMU can execute
virtual machines easily with a single command. We build all of this into a container image, so
that in essence, when the container is started, the virtual machine is started as well.

See :ref:`architecture <architecture>` for more details on this and other aspects of images
within Antidote.

Do you only support Junos?
~~~~~~~~~~~~~~~~~~~~~~~~~~

This is a common question we get because the only image currently in use in the NRE Labs curriculum
is the vQFX image, and of course Juniper is paying the cloud bills for the NRE Labs site, so this question
is a fair one.

Bottom line is, there's no architectural restriction against running other images. In fact, the platform was
built from day one to be multivendor, and not just in the fact we can run the image, but also in how it's
incorporated into the true value of the platform, such as autoconfiguration between labs.

The technical requirement is that the network device is accessible via SSH for terminal access with the
appropriate credentials and packaged within a docker container. We're already using NAPALM for doing
inter-stage configuration, so we're ready to use other vendor kit from the get-go; it's just a matter
of getting vendors to contribute their image. Juniper has done this as an early example, but any other
vendor that is willing to abide by the  :ref:`Code of Practice <code-practice>` is welcome to
participate in the project.

In short, we've put the right technical pieces in place to make it possible, now we're working on getting
other vendors to contribute images to be used in the platform.

How do I get my "stuff" into a lesson?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It's quite rare to have a lesson in mind that doesn't also include some kind of custom "thing".
This could be a simple script you wrote or downloaded and wish to show it in your lesson,
configuration or data files used by an application, or full-blown software you'd like to be
installed and running or available within the environment. At the end of the day,
your goal is to get this "stuff" into your lesson definition.

In the **vast majority of cases**, the best way to do this is simply to store those files in the
curriculum repo within your lesson directory. In    

it's a matter of just putting it in your lesson directory. The entire curriculum is mapped via volume
to every container that runs in a lesson, so just by having those files in that directory, you'll have access to them at runtime.

You can also create a docker image that follows the `image` (LINK) standards if you want a more complicated software installation to
be present.







# David Barosso Questions
1. is there more detailed documentation somewhere?
3. if I add a lesson, should I just number it and put it here? github.com/nre-learning/a…



Things from Dmitri Figol stream to fix
- Copy/paste from lesson guide
- Fix random disconnects after idling for a while
- Copying from robot file out of terminal strips newlines
- Install browser in utility so you can browse the report
- Consider disabling right click?
- Expand grafana iframe
- unexpected session close
- order of snippets in lab 2 of st2 lesson

