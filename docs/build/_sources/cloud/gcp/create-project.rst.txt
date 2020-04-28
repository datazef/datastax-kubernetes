Create a project
================

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`./login`

Procedure
---------
* From the Google console, create a project using the command:

.. code-block:: shell

   $> gcloud projects create datastax-1 --name="dsegke"

Post-requisites
---------------
* Check if the project was created successfully:

.. code-block:: shell
   :emphasize-lines: 3
   
   $> gcloud projects list
   PROJECT_ID             NAME               PROJECT_NUMBER
   datastax-1      dsegke  324324530958


