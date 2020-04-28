Configure project for kubernetes deployment
===========================================

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`./login`
* :doc:`./create-project`

Procedure
---------
* From the Google console, retrieve the project ID and launch the command:

.. code-block:: shell

   $> gcloud config set project datastax-273616

* To enable a specific API from the console for the project, just enable it:

.. code-block:: shell

   $> gcloud services enable container.googleapis.com

.. note::
   In order to get all services available, use the command: gcloud services list --available   

* Additional parameters liks zone can be configured as well:

.. code-block:: shell

   $> gcloud config set compute/zone us-west1

.. warning::
   * make sure the zone match the configuration of the cluster in the configuration file k8s-build/templates/cassandra/example-dse-full.yaml configuration file. In this version they are both configured to us-west1.


Post-requisites
---------------
* Verify the default project:

.. code-block:: shell
   :emphasize-lines: 2

   $> gcloud config get-value project
   datastax-273616

* Verify the default zone:

.. code-block:: shell
   :emphasize-lines: 2

   $> gcloud config get-value compute/zone
   us-west1

* Check if the container API can be used:   

.. code-block:: shell
   :emphasize-lines: 2, 3

   $> gcloud services list | grep container
   container.googleapis.com             Kubernetes Engine API
   containerregistry.googleapis.com     Container Registry API