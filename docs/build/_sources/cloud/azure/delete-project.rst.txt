Delete a project
================

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`./login`

Procedure
---------
* From the Google console, delete a project using the command:

.. code-block:: shell

   $> az aks delete --name myAKSCluster -g datastax-1


Post-requisites
---------------
* Check if the project was deleted successfully:

.. code-block:: shell

   $> az group list --query [*].name | grep datastax-1