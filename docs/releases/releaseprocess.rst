.. _release-process:

Antidote Release Process
================================

.. WARNING::
    
    This area is HEAVILY under construction. We're committing this to the docs for now as a
    placeholder, but will be contributing to it meaningfully over the next few releases.

First, run `make` and `make test` in Syringe, with a clean repo, up to date with `master` checked out.
Only if this passes, move on.

Generate Token for StackStorm
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. CODE::

    kubectl create sa stanley
    kubectl create clusterrolebinding owner-cluster-admin-binding \
        --clusterrole cluster-admin \
        --user stanley
    secret=$(kubectl get sa stanley -o json | jq -r '.secrets[0].name')
    kubectl get secret $secret -o json | jq -r '.data["token"]' | base64 -D
    kubectl get secret $secret -o json | jq -r '.data["ca.crt"]' | base64 -D > ca.crt

