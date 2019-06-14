.. _toolbox-presentation:

Endpoint Presentation
=====================


Must provide at least one presentation, OR at least one additionalPort.

Presentation Options
~~~~~~~~~~~~~~~~~~~~~

SSH
  **Usage:** ``configurationType: napalm-<driver>``


  In previous versions of the Antidote platform, this was the only option. It's a fairly easy way to
  get a config file from the repo onto a network device. While we've made improvements to this

  This doesn't just use NAPALM, but also does the templating thing with the env var

HTTP
  **Usage:** ``configurationType: python``

    Right now the endpoint must be http only. The traffic will be passed through the load balancer, which provides HTTPs.
    {Name: "SYRINGE_FULL_REF", Value: fmt.Sprintf("%s-%s", nsName, ep.GetName())},

VNC
  Not currently supported - coming soon!
