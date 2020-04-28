Install SDK
===========

.. note::
   Refer to Google main page for further information: https://cloud.google.com/sdk/docs/quickstart-macos.

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* Download gcloud sdk artifact for your platform.

Procedure
---------
* Untar the archive:

.. code-block:: shell

   $> tar xvzf google-cloud-sdk-289.0.0-darwin-x86_64.tar.gz

* Ideally update the .bash_profile to add the google cloud sdk binaries to your path

Post-requisites
---------------
* Verify the installation:

.. code-block:: shell
   :emphasize-lines: 2

   $> gcloud -v
   Google Cloud SDK 289.0.0
   bq 2.0.56
   core 2020.04.10
   gsutil 4.49

* To upgrade components:

.. code-block:: shell
   :emphasize-lines: 16

   $> gcloud components update
   Do you want to continue (Y/n)?  Y
   
   ╔════════════════════════════════════════════════════════════╗
   ╠═ Creating update staging area                             ═╣
   ╠════════════════════════════════════════════════════════════╣
   ╠═ Uninstalling: Cloud SDK Core Libraries                   ═╣
   ╠════════════════════════════════════════════════════════════╣
   ╠═ Installing: Cloud SDK Core Libraries                     ═╣
   ╠════════════════════════════════════════════════════════════╣
   ╠═ Creating backup and activating new installation          ═╣
   ╚════════════════════════════════════════════════════════════╝
   
   Performing post processing steps...done.                                                                                                                                                                                                                                             
   
   Update done!
