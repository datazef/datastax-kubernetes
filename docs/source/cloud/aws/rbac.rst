RBAC
====

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* Download aws sdk artifact for your platform.
* Download eksctl artifact for your platform

Procedure
---------
* Configure special RBAC for the APIs to properly operate:

.. code-block:: shell

   $> kubectl edit clusterrolebinding eks:node-manager

* Add the name of the namespace you want to work with in the subjects section as follow:

.. code-block:: shell
   
   subjects:
    - apiGroup: rbac.authorization.k8s.io
     kind: User
     name: eks:node-manager
     namespace: cass-operator

Post-requisites
---------------
* N/A