Delete cass-operator
====================

.. note::
   This is in addition to all notes available on DataStax https://docs.datastax.com/en/cass-operator/doc/cass-operator/cassOperatorTOC.html and to the information available https://github.com/datastax/cass-operator

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* GKE: :doc:`./install-cass-operator`

Procedure
---------
* Delete cassandra-operator:

.. code-block:: shell

   $> kubectl delete -f https://raw.githubusercontent.com/datastax/cass-operator/v1.4.0/docs/user/cass-operator-manifests-v1.15.yaml

Post-requisites
---------------


