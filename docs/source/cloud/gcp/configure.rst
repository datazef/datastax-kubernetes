****************
Configure gcloud
****************

Pre-requisites
##############
Before you start, make sure you have performed the following tasks:

* :doc:`./login`
* Have a project created using the web console or :doc:`./create-project` if you configure a project

Procedure
#########
* From the Google console, retrieve the project ID and launch the command:

.. code-block:: shell

   $> gcloud config set project datastax-273616

* Additional parameters liks zone can be configured as well:

.. code-block:: shell

   $> gcloud config set compute/zone us-west1


Post-requisites
###############
* Check if the project was created successfully:

.. code-block:: shell

   $> gcloud container clusters list
   NAME                                         STATUS   ROLES    AGE   VERSION
   gke-cluster-dse-default-pool-070d8a9f-l5j3   Ready    <none>   27m   v1.14.10-gke.27
   gke-cluster-dse-default-pool-070d8a9f-mg9p   Ready    <none>   27m   v1.14.10-gke.27
   gke-cluster-dse-default-pool-1798d660-fqtc   Ready    <none>   27m   v1.14.10-gke.27
   gke-cluster-dse-default-pool-1798d660-wz0r   Ready    <none>   27m   v1.14.10-gke.27
   gke-cluster-dse-default-pool-d339feaf-124r   Ready    <none>   27m   v1.14.10-gke.27
   gke-cluster-dse-default-pool-d339feaf-m54n   Ready    <none>   27m   v1.14.10-gke.27