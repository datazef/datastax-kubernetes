**********************************
Create a Kubernetes cluster in GCP
**********************************

Pre-requisites
##############
Before you start, make sure you have performed the following tasks:

* :doc:`./configure` if you do not want to repeat all parameters

Procedure
#########
* From the Google console, create a cluster using the command:

.. code-block:: shell

   $> gcloud container clusters create cluster-dse  --machine-type "n1-standard-1" --num-nodes "2"
   Creating cluster cluster-dse in us-west1... Cluster is being health-checked (master is healthy)...done.                                            Created [https://container.googleapis.com/v1/projects/fieldops-delivery/zones/us-west1/clusters/cluster-dse].
 
   NAME         LOCATION  MASTER_VERSION  MASTER_IP     MACHINE_TYPE   NODE_VERSION    NUM_NODES  STATUS
   cluster-dse  us-west1  1.14.10-gke.27  34.82.61.164  n1-standard-1  1.14.10-gke.27  15         RUNNING

.. note::
   For zone names and other, refer to: https://cloud.google.com/compute/docs/regions-zones#available.

.. warning::
   num nodes define the number of nodes per zone and not the total number of nodes


Post-requisites
###############
* Check if the project was created successfully:

.. code-block:: shell

   $> gcloud container clusters list
   NAME         LOCATION  MASTER_VERSION  MASTER_IP     MACHINE_TYPE   NODE_VERSION    NUM_NODES  STATUS
   cluster-dse  us-west1  1.14.10-gke.27  34.82.61.164  n1-standard-1  1.14.10-gke.27  6          RUNNING

