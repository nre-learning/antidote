.. _antidote-git:

Working with Antidote Git Repositories
======================================

The Antidote project does everything in the open. All configurations, curriculum resources, and source code
can be found in one of the GitHub repositories in the nre-learning organization. As a result, no matter where
you want to contribute to the Antidote project, you're likely able to do so by contributing to one of these repositories.

However, not everyone that wants to contribute knows how Git works, and even for those that do, the way the Antidote project uses Git to
accept contributions may not exactly match with previous experience. This document is aimed at covering everything you'll
need to know to contribute to any Antidote repository. Other pages within this documentation explain the specifics
of contributing to the curriculum, the underlying platform, the development environment, or even the documentation itself,
but they all have one common theme - at some point, in order to contribute, you will need to work with Git or Github.

So, those pages will focus on the specific details and repositories they cover, but will inevitably link here. So,
this document will apply to any Git repository those pages might reference, even though we'll use some specific
examples here for illustrative purposes.

.. NOTE::

    This is **not** meant to be a tutorial on Git or Github. While you certainly don't need to be a Git expert to
    work with Antidote repositories (especially if you're only interacting with Github), you will always be
    well-served to get some basics under your belt. This `basic introduction <https://git-scm.com/book/en/v1/Git-Basics>`_
    is highly recommended reading, and we will be making some references to the terms contained within.
    In addition, if you don't have a Github account, sign up for one `here <https://github.com/join>`_. There's really
    no getting around it, if you wish to interact with the Antidote project in nearly any capacity.

The `nrelabs-curriculum <http://github.com/nre-learning/nrelabs-curriculum>`_ repository is probably one of the most popular repositories
in the Antidote project. While not technically part of the Antidote platform, it is the flagship curriculum developed
for the platform, and is what powers the `NRE Labs <https://labs.networkreliability.engineering>`_ site. For the vast majority
of examples, we'll be using this repository to illustrate the concepts, but for the most part, everything applies to any Antidote
repository.

.. _git-watching:

"Watching" for Activity Notifications
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

One of the easiest ways to start getting involved with the Antidote project is to just pay close attention to what's going on.
In addition to making sure you're aware of new threads on the `community site <https://community.networkreliability.engineering/>`_
(which you should totally do), a leading way to do this is to "Watch" the Antidote repositories relevant to you. You can do this by navigating
to one of the repositories, and clicking the "Watch" drop-down at the top right of the page:

.. image:: /images/watch.png
   :align: center

Make sure you also take a look at your `notification settings <https://github.com/settings/notifications>`_ to ensure that not only are
you notified for new issues and Pull Requests, but also that the email address is one that you check often. Notifications at this level
are always relevant and technical, and represent the true nature of discussion going on with the project. So if you're willing to
turn notifications on for anything, this is the time to do it.

.. _git-issues:

How and When to Open an Issue
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Without a doubt, the `community site <https://community.networkreliability.engineering/>`_ is the best place to go for general
discussions and support with developing lessons, or even working with code on the Antidote platform. However, sometimes it's
necessary to make more of a definitive statement, such as "I think I'm encountering a bug, here's what I'm seeing", or "I
really with Antidote did X". In these cases, where such a statement may not have an immediate answer but clearly represents
some level of work to satisfy, a Github Issue is often the best place to post that.

.. NOTE::
    In some cases, project leaders will provide guidance when something is or isn't appropriate as a Github Issue. In fact, sometimes
    it's not immediately clear if an Issue is warranted until the conversation has taken place elsewhere first. In general,
    don't stress out too much about when something is or isn't appropriate as an Issue, but be willing to move where the conversation
    needs to go.

Issues aren't restricted only to folks to have pushed code or other content to a repository. If you have constructive feedback,
that is just as valuable a contribution, and opening a new Issue is a great way to do that. Examples include:

- Bug reports (even if you're not quite sure it's a bug)
- Feature requests
- Help with an error

Every repository has an "Issues" tab that you can click to take you to the currently open Issues for that repository:

.. image:: /images/issuetab.png
   :align: center

There's a big green button at the top left of that page (once you click the Issues tab) that said "New Issue".
Clicking that will take you to a form where you can provide a title and description. For some Antidote repositories,
these fields will be pre-populated with a framework of the kind of information that would be very helpful to anyone
that looks into things for you. In general, follow the guidance that's there, but post as much detail as you can, and
be ready to provide more if asked.

.. _git-lowhanging:

Using Issues to Identify Low-Hanging Fruit
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you have poked around at the open issues, you may notice that some of them have colorful tags attached to them.
Github calls these "labels", and they are useful for providing additional categorization for issues or pull requests.

Lots of folks approach open source projects with some enthusiasm and willingness to get involved, but often don't know
where to start. It's pretty difficult to look at a list of bug reports and have any idea how far the rabbit hole goes
for any of them. The best way to get started with a project is to take on a task that gets you that experience without
requiring you to spin your wheels for weeks, which is super demotivating.

For you, we've created complexity ratings in the form of Github Issue labels, and try our best to apply them to each
issue on the Antidote repositories:

.. image:: /images/complexitylabels.png
   :align: center

These are things like enhancements or bugfixes that we've set aside that are relatively approachable, and don't require
you to know how everything works in order to satisfy them. What this means for you, is you can easily get a
look at a repositories low-hanging fruit tasks by filtering issues by the ``complexity: low`` label.
For the ``nrelabs-curriculum`` repository, this URL gets you straight there:

`<https://github.com/nre-learning/nrelabs-curriculum/labels/complexity%3A%20low>`__

However, nearly all Antidote repositories have the same taxonomy, so no matter where your interests lie, this mechanism is
in place for you to identify those "entrance ramp" tasks. If you lean more towards web or front-end development, the `complexity: low
tag in antidote-web <https://github.com/nre-learning/antidote-web/labels/complexity%3A%20low>`_ may interest you.
If you like to work on back-end systems, or with languages like Python or Go, the `same tag in Syringe <https://github.com/nre-learning/antidote-web/labels/complexity%3A%20low>`_
may interest you.


Support? ask questions via the :ref:`community forums <community-forums>`,

.. _git-fork:

Making a Change to a Repository
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Eventually, you may get comfortable enough with a repository that you want to start making changes yourself. Maybe you
found an Issue in the previous section with a ``complexity: low`` label and you want to do the work to solve it.

The first thing you'll want to do is "Fork" the repository. You may have heard previously that this term has a little bit
of a negative connotation in open source. In this case, it's totally fine - forking is a common way of contributing to a
Github repository. In short, "Forking" creates a copy of a repository so that you can push directly to it. To do this,
click the "Fork" button in the top right of any repository:

.. image:: /images/fork.png

Next, Github will ask you where you want to place the fork. Remember, this is like making a copy, so it's asking where you want
the copy of that repository to go. Usually, people select their own username. Doing that will result in a repository under
your own Github username like so:

.. CODE::

    https://github.com/<your username here>/nrelabs-curriculum

Now that you have created a fork, you need to create a **local** copy of that fork so that you can actually work with the files.
This is called `"cloning" the repository <https://git-scm.com/book/en/v1/Git-Basics-Getting-a-Git-Repository#Cloning-an-Existing-Repository>`_.
There are a few ways to do this, but the easiest is to simply copy the URL of your forked repository, and type the following into a terminal window:

.. CODE::

    git clone <paste URL here>

This will result in a directory at that location named identically to the repository, such as ``nrelabs-curriclum``. The last thing
you'll probably want to do in order to get working is to create a branch. This isn't strictly necessary, since we're working
on a separate copy of the repository, but it's a good habit to get into, and lets you work on multiple things at once with your fork
if you decide to drink some Red Bull.

You can simultaneously create and check out a branch with:

.. CODE::

    git checkout -b new-branch-name

.. NOTE::

    Everything in this section so far should only need to be done once. However, everything else in this section may have to be
    repeated multiple times as you work through a change.

You're now ready to make changes to the files on your filesystem. Obviously, **what** you do here will vary wildly
depending on what you're trying to do and what repository you're working with. See the relevant documentation for that
side of things. Once you've made some changes, you might be wanting to save your progress in Git so that you can track
your progress. It's generally good practice to
`make commits <https://git-scm.com/book/en/v1/Git-Basics-Recording-Changes-to-the-Repository#Committing-Your-Changes>`_
somewhat often so that if you make mistakes, you can roll back easily.

Once you've made some commits, you'll want to `push` them. This ensures that the branch you have locally is replicated to your
fork:

.. CODE::

    git push origin <your branch>

Once you have commits pushed, you can open a Pull Request, which is a way of saying "I have changes in my fork that I would like you
to pull into the main repository". You can do this immediately, or after you feel like you're finished
with the work. Opening a Pull Request early, before you're finished with the work, is totally fine, as any subsequent commits pushed
to your branch will update the Pull Request. In addition, there are ways to open a Pull Request that lets folks know you're not quite
finished with the work - this is totally fine, and in fact encouraged.

If you navigate to the Github page for your fork, you'll notice that there's a little bar that says you're
X commits ahead of the main repository, with some buttons next to it that let you open a Pull Request:

.. image:: /images/branchchanges.png

Make sure the correct branch is selected in the drop-down to the left, and then click "Pull Request" on the right.
This will take you to the upstream repository to open a new Pull Request:

.. image:: /images/pullrequest.png

Be descriptive here - let folks know what you're working on and what stage it's in. Feel free to use the description
to summarize any outstanding work you have to do, if you're not quite finished.

Also - if you're not finished with the work, that's totally fine, but there are a few tricks you can use to make sure people
know that. For instance, putting "WIP" in the title, like in the screenshot above, is a good sign to others that you're still
working on it. Also, Github recently introduced a new feature for opening "draft" pull requests. In the screenshot above you
can also see a dropdown that lets you do this.

When you're ready for someone to review your work, remove any mentions of "WIP", and mark the PR ready for review.
