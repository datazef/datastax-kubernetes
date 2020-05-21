Create a Kubernetes cluster
===========================

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`./login`
* :doc:`./create-project`
* :doc:`./configure`

Procedure
---------
* From the Google console, create a cluster using the command:

.. code-block:: shell
   :emphasize-lines: 2, 5

   $> gcloud container clusters create cluster-dse  --machine-type "n1-standard-1" --num-nodes "2"
   Creating cluster cluster-dse in us-west1... Cluster is being health-checked (master is healthy)...done.                                            Created [https://container.googleapis.com/v1/projects/fieldops-delivery/zones/us-west1/clusters/cluster-dse].
 
   NAME         LOCATION  MASTER_VERSION  MASTER_IP     MACHINE_TYPE   NODE_VERSION    NUM_NODES  STATUS
   cluster-dse  us-west1  1.14.10-gke.27  34.82.61.164  n1-standard-1  1.14.10-gke.27  15         RUNNING

.. note::
   * For zone names and other, refer to: https://cloud.google.com/compute/docs/regions-zones#available.
   * If you want to use dse it is preferable to use a bigger instance type like n1-standard-1. Cassandra can be installed with smaller instances types. 
   * nodes will be created in the zone defined as default in the project settings. If desired otherwise, pass required arguments.

.. warning::
   * num nodes define the number of nodes per zone and not the total number of nodes 


Post-requisites
---------------
* Check if the cluster was created successfully:

.. code-block:: shell
   :emphasize-lines: 3

   $> gcloud container clusters list
   NAME         LOCATION  MASTER_VERSION  MASTER_IP     MACHINE_TYPE   NODE_VERSION    NUM_NODES  STATUS
   cluster-dse  us-west1  1.14.10-gke.27  34.82.61.164  n1-standard-1  1.14.10-gke.27  6          RUNNING

* To list all the nodes in the cluster:

.. code-block:: shell

   $> kubectl get nodes --label-columns failure-domain.beta.kubernetes.io/region,failure-domain.beta.kubernetes.io/zone | column -t
   gke-cluster-dse-default-pool-5833fc98-lcct  Ready   <none>  15m  v1.14.10-gke.27  us-west1  us-west1-c   gke-cluster-dse-default-pool-5833fc98-vl15  Ready   <none>  15m  v1.14.10-gke.27  us-west1  us-west1-c
   gke-cluster-dse-default-pool-6aae0f91-c6hv  Ready   <none>  15m  v1.14.10-gke.27  us-west1  us-west1-a
   gke-cluster-dse-default-pool-6aae0f91-n4pw  Ready   <none>  15m  v1.14.10-gke.27  us-west1  us-west1-a
   gke-cluster-dse-default-pool-8d04372a-psc3  Ready   <none>  15m  v1.14.10-gke.27  us-west1  us-west1-b
   gke-cluster-dse-default-pool-8d04372a-sg5k  Ready   <none>  15m  v1.14.10-gke.27  us-west1  us-west1-b


