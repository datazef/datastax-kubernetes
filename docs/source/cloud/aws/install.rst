Install SDK
===========

.. note::
   Refer to AWS main page for further information: https://docs.aws.amazon.com/cli and https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html#install-eksctl for eksctl installation

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* Download aws sdk artifact for your platform.
* Download eksctl artifact for your platform

Procedure
---------
* Install the provided artigfacts for you platform

Post-requisites
---------------
* Verify the installation of aws cli:

.. code-block:: shell
   :emphasize-lines: 2

   $> aws --version
   aws-cli/2.0.54 Python/3.7.4 Darwin/19.6.0 exe/x86_64

* Verify the installation of eksctl:

.. code-block:: shell
   :emphasize-lines: 2

   $> eksctl version
   0.29.0