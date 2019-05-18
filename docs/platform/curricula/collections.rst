Collections
=========================

With any curriculum, there are natural categorizations that arise from its content. For instance,
in the automation space, you have fundamental skills, tools, and then the application of those tools.
Further, you have categorization within each of those - maybe according to language or level of difficulty.

Sometimes a second axis of categorization is needed. Some lessons which have little to nothing
in common technically, are tightly aligned around some other theme. For instance, a group of technically unrelated lessons
might all be contributed by the same organization, and it would be nice to be able to see them all in one place, with some
references to where users can learn more about that organization. Or maybe some lessons operate under some kind of constraint,
such as only being useful on a certain vendor's equipment.

Enter collections. These are a new resource type in Syringe that allows you to define all of the metadata necessary for describing
such a grouping. Just like other resource types, collections are defined in a simple YAML definition, and Antidote takes care of
nicely rendering it in the web UI:

.. image:: /images/collections.png



Once defined, other resources like lessons are able to reference the ID(s) of the collection they belong to, if applicable.

.. NOTE::

  An important note, especially if you're looking to create a collection for your company. This is totally acceptable - nay,
  encouraged - as long it's done the right way. Collections aren't a sales pitch. You can talk about your company and give a
  brief overview, but stay away from language like "we're the best" in favor of simply and succinctly describing what you do,
  why you have contributed to NRE Labs, and what users can expect to see from you here.

Collections Definitions
^^^^^^^^^^^^^^^^^^^^^^^

Defining a collection is fairly straightforward. There's a bit of metadata, and a few description fields for you to populate.
There are also some fields for pointing users to a relevant website or contact email, where appropriate. This is useful to give users
a place to go after they find your content, and want to find out more about the person or organization behind it.

.. CODE:: yaml

  ---
  id: 1
  title: Juniper Networks
  image: https://raw.githubusercontent.com/nre-learning/nrelabs-curriculum/master/collections/juniper/juniper.png
  website: https://juniper.net
  contactEmail: "support@juniper.net"

  # Why should users view your collection?
  briefDescription: Juniper exists to solve the world’s most difficult problems in networking. Today, complexity is at the heart of those problems. Simple is our obsession. And simple always starts with engineering. This collection contains curriculum resources contributed by Juniper, or lessons that deal mostly in Juniper-specific technology.

  # Why should users continue and view your lessons?
  longDescription: | 
    Juniper is responsible for starting the Antidote project and offering the NRE Labs site free of charge to all who wish to learn automation with as few barriers as possible. The original spirit of NRE Labs is to focus on bringing network engineering skillsets into the cloud era, by focusing on individual success, even if it means a multi-vendor approach.

    There are a number of tools and projects - even open source, that while useful, are mostly usable only within a Juniper context. For instance, the JSNAPy project is an open source tool that allows engineers to write unit tests for their Junos network devices. While this tool is free and open source, it's also Juniper-specific, and we want to be up-front about that.

    To remain loyal to the spirit of NRE Labs, we created this collection so that the learner can be made aware of content that may be either mostly or entirely useful within a Juniper context, on Juniper devices and software.

  type: vendor

  # Similar to lesson definition "tier" field. Can be "prod" or "ptr"
  tier: prod

This collection definition is just an example. You should look at the `existing collection definitions <https://github.com/nre-learning/nrelabs-curriculum/tree/master/collections>`_ for inspiration. Note also that
not every field picture above is required. Some are optional. Using the :ref:`syrctl validate command <syrctl-validate>` will be useful for identifying which fields
you need to provide no matter what.

As with lesson definitions, follow the :ref:`NRE Labs curriculum contribution guide <contrib-curriculum>` in order to get your collection added to the NRE Labs curriculum.