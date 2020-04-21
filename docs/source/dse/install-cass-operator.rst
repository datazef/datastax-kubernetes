*********************
Install cass-operator 
*********************

.. note::
   This is in addition to all notes available on DataStax https://docs.datastax.com/en/cass-operator/doc/cass-operator/cassOperatorTOC.html and to the information available https://github.com/datastax/cass-operator

Pre-requisites
##############
Before you start, make sure you have performed the following tasks:

* GKE: :doc:`../cloud/gcp/create-cluster` and :doc:`../cloud/gcp/connect-cluster`

Procedure
#########
* Deploy the cass-operator:

.. code-block:: shell

   $> kubectl apply -f https://raw.githubusercontent.com/datastax/cass-operator/26ad52bfc8f450852f5573fa2904a5df407ce2d3/docs/user/cass-operator-manifests.yaml
   namespace/cass-operator created
   serviceaccount/cass-operator created
   role.rbac.authorization.k8s.io/cass-operator created
   rolebinding.rbac.authorization.k8s.io/cass-operator created
   customresourcedefinition.apiextensions.k8s.io/cassandradatacenters.cassandra.datastax.com created

This command will create the following:

:namespace: Creation of the namespace `cass-operator`
:ServiceAccount: Creation of the service account `cass-operator` in the namespace `cass-operator`
:Role: Creation of the role `cass-operator` in the namespace `cass-operator`
:RoleBinding: Bind the role `cass-operator` in the namespace `cass-operator` to service account `cass-operator`
:Resources: CassandraDatacenter interface
:Deployment: define deployment for the cass-operator docker

Post-requisites
###############
* Check if all resources are created:

.. code-block:: shell

   $> kubectl get serviceaccounts --namespace=cass-operator
   NAME            SECRETS   AGE
   cass-operator   1         9m57s
   default         1         9m57s

   $> kubectl get pods --namespace=cass-operator
   NAME                             READY   STATUS    RESTARTS   AGE
   cass-operator-65cf9cf944-vg9bb   1/1     Running   0          3m16s

