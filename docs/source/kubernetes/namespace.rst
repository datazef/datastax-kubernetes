********************
Namespace cheatsheet 
********************

Pre-requisites
##############
Before you start, make sure you have performed the following tasks:

* GKE: :doc:`../cloud/gcp/create-cluster` and :doc:`../cloud/gcp/connect-cluster`

Procedure
#########
* List resources:

.. code-block:: shell

   $> kubectl get {namespaces|pods|nodes|serviceaccounts} --namespace=cass-operator
   NAME              STATUS   AGE
   cass-operator     Active   3m4s
   default           Active   76m
   kube-node-lease   Active   76m
   kube-public       Active   76m
   kube-system       Active   76m 


Post-requisites
###############

