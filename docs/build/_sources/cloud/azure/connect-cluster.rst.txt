Connect kubectl to a k8s cluster
================================

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`./create-cluster`

Procedure
---------
* From the Azure CLI, connect to a cluster using the command:

.. code-block:: shell

   $> az aks get-credentials --resource-group datastax-1 --name myAKSCluster


.. note::
   Make sure you use the correct resource group and AKS name


Post-requisites
---------------
* Check if connection is successful:

.. code-block:: shell
   :emphasize-lines: 2,3, 4, 5, 6

   $> kubectl get nodes
   NAME                       STATUS   ROLES   AGE   VERSION
   aks-nodepool1-99674446-0   Ready    agent   20h   v1.15.10
   aks-nodepool1-99674446-1   Ready    agent   20h   v1.15.10
   aks-nodepool1-99674446-2   Ready    agent   20h   v1.15.10
   aks-nodepool1-99674446-3   Ready    agent   20h   v1.15.10

.. note::
   From here you can use the cluster with the kubecl command utility ;-)