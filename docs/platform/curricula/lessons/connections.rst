.. _toolbox-connections:

Connections
===========

Another cool thing about Antidote is that it allows lesson creators to build complex topologies of
Endpoints through some simple back-end networking orchestrated by :ref:`Syringe <syringe>`_ and made possible by Kubernetes
and a special networking plugin.

We explain **how** this all works over in the :ref:`Architecture docs <architecture>`. The way you use this functionality in a lesson
is fairly simple. The first thing you should know is that all Endpoints are connected to the same "management" network. The ``eth0``
interface of every container is connected here, and each can communicate with each other by default.

The example below shows three Endpoints in a lesson definition:

.. CODE:: yaml

  endpoints:
  - name: vqfx1
    image: antidotelabs/vqfx:snap1
    configurationType: napalm-junos
    presentations:
    - name: cli
      port: 22
      type: ssh

  - name: vqfx2
    image: antidotelabs/vqfx:snap2
    configurationType: napalm-junos
    presentations:
    - name: cli
      port: 22
      type: ssh

  - name: vqfx3
    image: antidotelabs/vqfx:snap3
    configurationType: napalm-junos
    presentations:
    - name: cli
      port: 22
      type: ssh

You can thing of these like nodes in a graph topology, as all networks are. So, if Endpoints are nodes, then the edges, or the connections
between these nodes, are ``connections``:

.. CODE:: yaml

    connections:
    - a: vqfx1
      b: vqfx2
    - a: vqfx2
      b: vqfx3
    - a: vqfx3
      b: vqfx1

This is a simple list of connections from ``a`` to ``b``. The first connection is from ``vqfx1`` to ``vqfx2`` and so on.
The back-end orchestrator will create virtual networks for each Connection, and then attach Endpoints to them.

You can see the attachment to these networks by describing any Kubernetes pod using the ``kubectl`` CLI that represents
an Endpoint:

.. CODE::

    kubectl -n=12-abcdefghijkl-ns describe pod vqfx1
    Name:               vqfx1
    Namespace:          12-abcdefghijkl-ns
    Priority:           0
    PriorityClassName:  <none>
    Node:               antidote-worker-6l0v/10.138.0.7
    Start Time:         Sun, 16 Jun 2019 22:16:16 -0700
    Labels:             lessonId=12
                        podName=vqfx1
                        syringeManaged=yes
    Annotations:        k8s.v1.cni.cncf.io/networks: [{"name":"vqfx1-vqfx2-net"},{"name":"vqfx3-vqfx1-net"}]
                        k8s.v1.cni.cncf.io/networks-status:
                        [{
                            "name": "",
                            "ips": [
                                "10.32.29.138"
                            ],
                            "default": true,
                            "dns": {}
                        },{
                            "name": "12-abcdefghijkl-ns-vqfx1-vqfx2-net",
                            "ips": [
                                "10.10.0.2"
                            ],
                            "dns": {}
                        },{
                            "name": "12-abcdefghijkl-ns-vqfx3-vqfx1-net",
                            "ips": [
                                "10.10.0.2"
                            ],
                            "dns": {}

As mentioned previously, the first interface/network is always the "management" network, and since ``vqfx1`` was a member of two
defined Connections, it has two additional networks.
