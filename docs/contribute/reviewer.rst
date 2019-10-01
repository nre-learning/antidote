.. _curriculum-reviewers:

Curriculum Review Standards
===========================

**ALL** contributions to the NRE Labs curriculum must be done via a Pull Request, and Pull Requests
can only be merged to ``master`` if the latest commit:

1. Passes all Github CI checks
2. Has a valid "accepted" review from a curriculum committer that is different from the PR creator.

At this point, the next step is for a reviewer to approve or make suggestions for a second round of edits
for your content. Note that the goal for **each and every review** is not to nitpick or make it difficult to
contribute to NRE Labs, but rather to ensure the content is reflected in the best light possible. Be patient
and willing to adapt to feedback.

Here are a few things that reviewers should be on the lookout for when reviewing new contributions to the
curriculum, either for new or existing lessons. If you're contributing to the curriculum, you should be aware
of these guidelines, to make the review process much smoother.

(Hopefully) Automated Checks
----------------------------

The following should be automatically checked via the CI tooling, but please double-check, and if the CI tooling
missed any of the below, please open an issue on the curriculum repo.

- Is the CHANGELOG updated properly?
- Does ``syrctl validate`` pass?

New Content Guidelines
----------------------

- Is the business benefit clear from this lesson? How easy is it for people
  to link this content with their day-to-day?
- Can a user get through a lesson stage quickly? Are we letting them get to a
  quick win as soon as practical while still teaching quality content?
- Does the new or changed lesson adhere to the spirit of Antidote lessons
  laid out in this document?
- For new lessons, does the lesson guide (or jupyter notebook if
  applicable) look nice? Does the author attribute themselves?
- Is the lesson guide(s) easy to follow?

Technical
---------

- Does this follow the :ref:`Lesson Image Requirements <lessonimages>`?
- Does the lesson appropriately take advantage of Antidote's optional features for content depth (like
  optional objective verification) or diverse presentations?

Logistics
---------

- Are any documentation updates also needed?
- Can we show this in NRE labs? Usage rights?