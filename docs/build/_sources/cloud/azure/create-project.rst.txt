Create a project
================

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`./login`

Procedure
---------
* From the Azure console, create a project using the command:

.. code-block:: shell

   $> az group create --name datastax-1 --location eastus
   

Post-requisites
---------------
* Check if the project was created successfully:

.. code-block:: shell
   :emphasize-lines: 3
   
   $> az group list --query [*].name
   [
	  "datastax-1",
	  "DefaultResourceGroup-EUS",
	  "cloud-shell-storage-eastus",
	  "MC_testGroup_myAKSCluster_eastus",
	  "NetworkWatcherRG"
   ]
  
