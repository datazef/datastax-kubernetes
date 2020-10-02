Create a Kubernetes cluster
===========================

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`./login`

Procedure
---------
* Using eksctl utility, create a cluster using the command:

.. code-block:: shell

   $> eksctl create cluster --name k8s --version 1.17 --region us-west-1 --nodes=6

aws ec2 describe-availability-zones --region us-west-2



Post-requisites
---------------
* Check if the cluster was created successfully:

.. code-block:: shell

   $> eksctl get cluster --name=k8s --region=us-west-1 


.. code-block:: shell

   $> eksctl utils describe-stacks --region=us-west-1 --cluster=k8s
   

