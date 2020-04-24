Connect kubectl to a specific k8 cluster
========================================

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`./create-cluster`

Procedure
---------
* From the Google console, create a cluster using the command:

.. code-block:: shell

   $> gcloud container clusters get-credentials cluster-dse --project fieldops-delivery --zone us-west1
   Fetching cluster endpoint and auth data.
   kubeconfig entry generated for cluster-dse.

.. note::
   Make sure you use the good cluster name, project name and zone


Post-requisites
---------------
* Check if connection is successful:

.. code-block:: shell

   $> kubectl get nodes
   NAME                                         STATUS   ROLES    AGE   VERSION
   gke-cluster-dse-default-pool-070d8a9f-l5j3   Ready    <none>   27m   v1.14.10-gke.27
   gke-cluster-dse-default-pool-070d8a9f-mg9p   Ready    <none>   27m   v1.14.10-gke.27
   gke-cluster-dse-default-pool-1798d660-fqtc   Ready    <none>   27m   v1.14.10-gke.27
   gke-cluster-dse-default-pool-1798d660-wz0r   Ready    <none>   27m   v1.14.10-gke.27
   gke-cluster-dse-default-pool-d339feaf-124r   Ready    <none>   27m   v1.14.10-gke.27
   gke-cluster-dse-default-pool-d339feaf-m54n   Ready    <none>   27m   v1.14.10-gke.27

.. note::
   From here you can use the cluster with the kubecl command utility ;-)