Login
=====

.. note:: 
   Refer to Get started with Azure CLI page: https://docs.microsoft.com/en-us/cli/azure/get-started-with-azure-cli?view=azure-cli-latest

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`./install`

Procedure
---------
* Login using the azure command:

.. code-block:: shell

   $> az login


Post-requisites
---------------
* Verify if authentication was successful:

.. code-block:: shell

   $> az account get-access-token

* Verify the account used:

.. code-block:: shell
   :emphasize-lines: 5

   $>  az account list --query [*].user
   
   [
   	{
    "name": "email@outlook.com",
    "type": "user"
    }
   ]


