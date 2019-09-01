.. _release-planning-curriculum:

Release Planning - Curriculum
================================

The lifecycle of a release of the curriculum is performed in four discrete steps, which are outlined
in the following sections.


Step 1 - Release Kickoff
------------------------

At the beginning of a release cycle, we'll have a "kickoff" during one of the weekly standups. This kickoff
is primarily focused on establishing the basic parameters of the release, beginning the process of gathering
deliverables intended for the release, and to ensure everyone knows where to find the latest
information on progress. 

In this first kickoff, we'll begin gathering ideas for things we want to get done in this release.
These will be retrieved from various sources:

- Open issues or PRs in the curriculum repo - comb and triage; Which are ready to be worked on, or are most imminent?
- Ideas from the community not yet documented formally
- Tasks needed for updating the curriculum to be compatible with a new platform version (if applicable)
- Any tasks that need to be done to bring the existing curriculum in line with the targeted Antidote platform
  version

While the kickoff is meant to get a starter list together, it's likely that more ideas will come up at any
time in the release cycle. This is normal, and expected. However, the first week of a release cycle should
strive to ensure the really important things are well-documented and if possible, assigned.

Another very important task for this initial meeting is to decide which Antidote
platform this curriculum release will :ref:`target <platform-targeting>`. If a new version is desired,
:ref:`PTR <ptr>` will be immediately updated to that stable release at the beginning of the
curriculum development cycle. Similarly, the :ref:`selfmedicate development environment <selfmedicate>`
should also be updated with this version, and curriculum developers should re-pull on this repository
to get the latest manifests.

A project plan for the release that represents the work discussed in the previous
week will be posted to the `curriculum repo's projects list <https://github.com/nre-learning/nrelabs-curriculum/projects>`_
and presented to attendees. This is a kanban-board style project planning tool that allows all to easily
see the state of work for a given release.

Finally, a post will be created in the `Curriculum Project Management
<https://community.networkreliability.engineering/c/curriculum-project-management>`_ topic to notify
everyone that the work on this release has begun, with the title "Release Kickoff...". This forum thread
should serve as the center of all release planning discussions, and all are welcome to participate. If you
have something you think should be included in or excluded from the release plan, speak up there.

.. NOTE::

    Not all work fits neatly into a release plan, and that's okay. Especially in the curriculum,
    contributions of any kind can reasonably take place at any time. The purpose of a release
    plan isn't to put limits on the work that can be done for a release, but rather to ensure
    that the important things that really **need** to get done are accounted for. If you want to
    work on something that's not explicitly asked for in the release plan, that's totally fine.

Step 2 - Development Work
-------------------------

Once a release cycle is kicked off, the only thing left to do is....do the work!
At this point, a relatively complete list of things to do for this release should be captured
in a Github project, which will be linke
.. _release-planning-platform-step-1:d to in the community forum kickoff post. Contributors
can use this as a guide, or do other work they think is useful.

The :ref:`curriculum contribution guide <contrib-curriculum>` should be consulted repeatedly
to ensure you're on the right track with respect to curriculum contributions. All of those guidelines
apply here. It's important for contributions to follow this lifecycle, so that release managers can properly
coordinate work across the project.

The :ref:`selfmedicate development environment <selfmedicate>` should also be used to locally
preview curriculum content that is being developed.

Step 3 - Testing Phase
----------------------

At some point, the list of tasks that are meant to be tackled for a given release are complete, and it's
time to initiate the process of cutting a release, and getting it into production.

The first step in this process is to ensure the latest changes in the ``master`` branch of the curriculum
are properly represented in the :ref:`PTR <ptr>`. This should automatically happen nightly, but someone from the NRE Labs Ops
team will make sure this is true.

A forum topic will be posted to `Curriculum Project Management
<https://community.networkreliability.engineering/c/curriculum-project-management>`_ with the title
"Testing Curriculum Release vX.X.X". This will contain a link to the testing procedure, and a summary of the
CHANGELOG at that point in time, so that new content can be tested properly. For a minimum of seven days from
the date of the post, contributors should test the site as it exists in :ref:`PTR <ptr>`, and submit feedback.

The best way to provide feedback is via a response to that original forum topic, or a Github issue
in the curriculum repository.

.. NOTE::

    Instead of submitting feedback, you may feel like you can just fix it yourself in a Pull Request.
    This is always welcome and appreciated, and is often the easiest way to make your first contribution
    to the curriculum. So, don't be shy! See the :ref:`curriculum contribution guide <contrib-curriculum>`
    for more info on how to do this.

The curriculum maintainers will stay on top of feedback and strive to ensure that all problems are either
fixed via a Pull Request, or documented via an Issue for a future release. The Testing Phase will not end
until the maintainers are comfortable that the latest ``master``, as represented via the :ref:`PTR <ptr>`
site represents a healthy curriculum.

Step 4 - Release and Deployment
-------------------------------

Once the testing phase has completed, the NRE Labs Ops team will execute a workflow that creates the target
version release for the curriculum, and will deploy this version to production.

In addition, if this curriculum release is meant to target a new version of the Antidote platform, the production
site should also be updated accordingly. 

In the following week (or at most two), the cycle will repeat, and a new release kickoff will take place.


.. _ptr:

Appendix - NRE Labs' "Public Test Realm"
----------------------------------------

To allow the community to see the latest changes in the curriculum, and help with testing them to ensure
they're solid before going into production, a
`"public test realm" (PTR) <https://ptr.labs.networkreliability.engineering>`_
is maintained separately from the production site. It can be thought of as a daily-updated release candidate for
the NRE Labs curriculum.

.. NOTE::

    PTR is **not** meant to be used to test Antidote platform features. Both the production and PTR
    sites will be running the latest stable release of the Antidote platform for which a stable
    version of the curriculum has been released. The idea of PTR is to provide a sort of rolling release
    candidate for the curriculum itself.

The PTR is redeployed nightly from the latest ``master`` of the NRE Labs
curriculum. This means that content that's gone through the proper approval process should show up
automatically within 24 hours.

As a result, PTR is inherently not guaranteed to be stable, and content in PTR should not be thought of as
"perfect". PTR is merely a representation of the current ``master`` branch of the curriculum - and because of that
, it's gone through at least one level of review. However, the presence of content in PTR is not an indication that
the content is ready for production.

The flow of content from contribution to PTR is outlined below:

.. image:: /images/ptr_process.png

As outlined in the previous sections, the curriculum is built to target a particular stable version of the
Antidote platform. Since the PTR is primarily used as a function of the curriculum, when a new curriculum
release cycle kicks off, and a platform version is identified, this version will be deployed to the PTR.

All curriculum content contains a ``tier`` field, which can be set to ``ptr`` in order to ensure that the content
only shows on the PTR. If content is deemed to be ready for production, it will be "promoted" by setting this field
to ``prod``. Note that content with a ``prod`` tier must still be captured into a stable release to actually make
it to the production site.

.. _platform-targeting:

Appendix - Platform Targeting
-----------------------------

The NRE Labs curriculum is released separately from the underyling Antidote platform. As a result,
the platform's release cycle will charge ahead with new features, and it's up to the curriculum release
planning to "target" a stable version of the platform to develop against. The below image shows an
**example** of how this might work:

.. image:: /images/curriculum_target.png

At the time the curriculum started on its own release cycle, ``v0.4.0`` of the platform was
released simultaneously with ``v1.0.0`` of the NRE Labs curriculum. In the future, the curriculum
may want to release a new version before ``v0.5.0`` of the platform is ready. In this case,
the curriculum, starting with ``v1.1.0`` will continue to target ``v0.4.0`` until a suitable
stable platform release is ready.