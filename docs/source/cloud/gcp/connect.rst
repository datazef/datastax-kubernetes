*********************************
Connect to a google cloud project
*********************************

Pre-requisites
##############
Before you start, make sure you have performed the following tasks:

* :doc:`./login`
* Have a project created using the web console or :doc:`./create-project`

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
