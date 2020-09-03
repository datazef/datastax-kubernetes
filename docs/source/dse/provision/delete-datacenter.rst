Delete datacenter
=================

.. warning::
   This will delete all data...


Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* GKE: :doc:`./create-datacenter`

Procedure
---------
* Delete all DC pods:

.. code-block:: shell

   $> kubectl delete cassdcs -n cass-operator dc1

Post-requisites
---------------
* Check if the cluster was properly deleted:

.. code-block:: shell
   :emphasize-lines: 2

   $> kubectl get cassdcs  -n cass-operator
   No resources found in cass-operator namespace.