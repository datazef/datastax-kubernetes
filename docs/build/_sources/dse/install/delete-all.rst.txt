Delete all
==========

.. warning::
   This will delete all data...


Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* GKE: :doc:`../../cloud/gcp/create-cluster` and :doc:`../../cloud/gcp/connect-cluster`

Procedure
---------
* Delete all DC pods:

.. code-block:: shell

   $> kubectl delete cassdcs --all-namespaces

Post-requisites
---------------


