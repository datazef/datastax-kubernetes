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

   $> gcloud projects delete datastax-1


Post-requisites
---------------
* Check if the project was deleted successfully:

.. code-block:: shell

   $> gcloud projects list | grep datastax-1