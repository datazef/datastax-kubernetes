Create a Kubernetes cluster
===========================

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`./login`
* :doc:`./create-project`

Procedure
---------
* From the Azure CLI, create a cluster using the command:

.. code-block:: shell

   $> az aks create --resource-group datastax-1 --name myAKSCluster --node-count 4 --enable-addons monitoring --generate-ssh-keys --node-vm-size Standard_DS4_v2
   

.. note::
   
   * If you want to use dse it is preferable to use a bigger instance types like Standard_DS4_v2. Cassandra can be installed with smaller instances types.
   * To get a list of fully supported Azure VM Skus run: "az vm list-skus --location eastus --query [*].name"



Post-requisites
---------------
* Check if the cluster was created successfully:

.. code-block:: shell
   :emphasize-lines: 4

   $> az aks list -o table
   Name          Location    ResourceGroup    KubernetesVersion    ProvisioningState    Fqdn
   ------------  ----------  ---------------  -------------------  -------------------  ----------------------------------------------------------
   myAKSCluster  eastus      datastax-1       1.15.10              Succeeded            myaksclust-datastax-1-c5058a-d170d212.hcp.eastus.azmk8s.io


