.. _contrib-nondev:

I'm Not a "Developer". How Can I Contribute?
============================================

For the NRE Labs project as a whole, putting everything in Git is
central to the spirit of the project. “Curriculum as Code” is part of what makes
NRE Labs tick - instead of storing the curriculum behind closed doors, it's
published for all to not only see, but also contribute to.

We've taken this idea and extended it to all aspects of the project, not just the
curriculum, or the technical bits of the Antidote platform. **Everything** we do
is represented in a Github repo somewhere under the ``nre-learning`` org. For example:

- The `NRE Website and Blog <https://networkreliability.engineering/>`_ is powered by
  software called Hugo, which takes simple Markdown files located in our `nre-blog repo <https://github.com/nre-learning/nre-blog>`_
  and renders them automatically into static HTML pages. This makes the blog much easier to manage,
  while also allowing folks to contribute without having to be web developers.
- All of our documentation is stored within the `docs directory of the Antidote repository <https://github.com/nre-learning/antidote/tree/master/docs>`_.
  Similar to the way our Blog works, this repo houses simple restructured text files that are converted to HTML
  by a service called Read The Docs, resulting in the `docs you see today <https://antidoteproject.readthedocs.io>`_.
- Our governance and technical planning docs are written in Markdown and added as Pull Requests to the
  `proposals repository <https://github.com/nre-learning/proposals>`_. Not only does this allow anyone to easily
  contribute to these, but this public model means all can participate in their formation. Pull Requests here
  are open to all to review at any time.

The end result of this is a model that is public and open to all by default. No matter what you're talking about,
whether core platform software, or blogs on the latest developments in the world of DevOps and NRE, it's all done
on Github.

That said - it might be easy to assume that you have to have a developer skill-set in order to work with Github.
Not so! You just need some tools and a little knowledge about plaintext formatting languages, which are outlined
below.

What You Need
-------------

First, you need to install two things on your computer:

- A decent text editor. I recommend `VSCode <https://code.visualstudio.com/download>`_ - it's free, simple enough while still being robust, and includes support
  for the things we will want to use it for.
- The `Github client <https://desktop.github.com/>`_. This is also cross-platform, and gives you the benefits of Github without having to do anything
  on the command-line.

Next, as all of the above projects use some kind of plaintext formatting language, you should do some basic
learning of the following:

- `Markdown <https://guides.github.com/features/mastering-markdown/>`_ - this is a plaintext formatting language that lets you do basic formatting like headers, lists,
  images, etc in a plaintext format. This allows us to very easily store the source of these files in Github
  but also convert them to something that looks properly formatted when we need to. The vast majority of the project
  uses Markdown for plaintext formatting.
- `Restructured Text (RST) <https://thomas-cokelaer.info/tutorials/sphinx/rest_syntax.html>`_ - this is similar
  to Markdown in that it's a plaintext formatting language, but it uses a different syntax from Markdown. The only
  place we use this is in the Antidote documentation. In fact, `this page is written in Restructured Text <https://raw.githubusercontent.com/nre-learning/antidote/master/docs/contribute/nondev.rst>`_!

Those are the basics. If you would like to see a walkthrough of these in action, please see the below video where
I go a lot deeper:

.. raw:: html

    <div style="text-align:center;"><iframe width="560" height="315" src="https://www.youtube.com/embed/YrajaNh_bJ0" frameborder="0" allowfullscreen></iframe></div>

Once you feel comfortable with the above, you can use the documentation on
":ref:`how to work with Antidote git repositories <antidote-git>`" for more info on how we use Github.

If you're working with the documentation, :ref:`we have detailed documentation <contrib-docs>` for
how to build that locally and preview it.
