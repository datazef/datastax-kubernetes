***************
Delete all DCs! 
***************

.. note::
   This is in addition to all notes available on DataStax https://docs.datastax.com/en/cass-operator/doc/cass-operator/cassOperatorTOC.html and to the information available https://github.com/datastax/cass-operator

Pre-requisites
##############
Before you start, make sure you have performed the following tasks:

* GKE: :doc:`../cloud/gcp/create-cluster` and :doc:`../cloud/gcp/connect-cluster`

Procedure
#########
* Delete all DC pods:

.. code-block:: shell

   $> kubectl delete cassdcs --all-namespaces

Post-requisites
###############


