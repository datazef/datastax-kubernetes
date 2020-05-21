Install SDK
===========

.. note::
   Refer to Azure CLI page for further information: https://docs.microsoft.com/en-us/cli/azure/install-azure-cli.

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* Download azure cli artifact for your platform.

Procedure
---------
* Install the azure-cli on Mac (See Azure site for Platform specific instructions):

.. code-block:: shell

   $> brew update && brew install azure-cli



Post-requisites
---------------
* Verify the installation:

.. code-block:: shell
   :emphasize-lines: 2,4,5,6,7

   $> az -v
   azure-cli                         2.0.74

   command-modules-nspkg              2.0.3
   core                              2.0.74
   nspkg                              3.0.4
   telemetry                          1.0.3

* To listinstall/update extensions:

.. code-block:: shell

   $>  az extension list-available --output table
   $>  az extension add --name <name from table>
   $>  az extension update --name <name from table>
  
   	   
   
