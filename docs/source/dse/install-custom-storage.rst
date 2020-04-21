**********************
Install custom storage 
**********************

.. note::
   This is in addition to all notes available on DataStax https://docs.datastax.com/en/cass-operator/doc/cass-operator/cassOperatorTOC.html and to the information available https://github.com/datastax/cass-operator

Pre-requisites
##############
Before you start, make sure you have performed the following tasks:

* GKE: :doc:`../cloud/gcp/create-cluster` and :doc:`../cloud/gcp/connect-cluster`

Procedure
#########
* Deploy the optimized storage class:

.. code-block:: shell

   $> kubectl apply -f https://raw.githubusercontent.com/datastax/cass-operator/26ad52bfc8f450852f5573fa2904a5df407ce2d3/operator/k8s-flavors/gke/storage.yaml
   storageclass.storage.k8s.io/server-storage created

Post-requisites
###############


