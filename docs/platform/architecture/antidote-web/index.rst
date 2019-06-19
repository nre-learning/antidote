.. antidoteweb:

Antidote-Web - Antidote's Front-End
===================================

This is the Web application facing the users, which will provide
access to Lesson resources in an integrated Web page.

Internally, it uses the Kubernetes reverse proxy to provide access to
Web applications PODs running directly inside the platform, and
`Guacamole <https://guacamole.apache.org/>`_ to provide terminal emulation for SSH connections to lesson nodes.

TBC
