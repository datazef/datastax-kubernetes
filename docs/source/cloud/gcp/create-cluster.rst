**********************************
Create a Kubernetes cluster in GCP
**********************************

Pre-requisites
##############
Before you start, make sure you have performed the following tasks:

* :doc:`./connect`

Procedure
#########
* From the Google console, create a cluster using the command:

.. code-block:: shell

   $> gcloud container clusters create cluster-dse  --machine-type "n1-standard-1" --num-nodes "4"

.. note::
   For zone names and other, refer to: https://cloud.google.com/compute/docs/regions-zones#available


Post-requisites
###############
