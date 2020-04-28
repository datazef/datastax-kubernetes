Login
=====

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`./install`

Procedure
---------
* Login using the gcloud command:

.. code-block:: shell

   $> gcloud auth login

* Set the account you want to use:

.. code-block:: shell

   $> gcloud config set account 'email@gmail.com'

Post-requisites
---------------
* Verify if authentication was successful:

.. code-block:: shell

   $> gcloud auth print-identity-token

* Verify the account used:

.. code-block:: shell
   :emphasize-lines: 2

   $> gcloud config get-value account
   email@gmail.com

