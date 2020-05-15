Install cass-operator 
=====================

.. note::
   This is in addition to all notes available on DataStax https://docs.datastax.com/en/cass-operator/doc/cass-operator/cassOperatorTOC.html and to the information available https://github.com/datastax/cass-operator

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* GKE: :doc:`../../cloud/gcp/create-cluster` and :doc:`../../cloud/gcp/connect-cluster`

Procedure
---------
* Deploy the cass-operator:

.. code-block:: shell
   :emphasize-lines: 2, 3, 11

   $> kubectl create -f k8s-build/templates/cassandra/cass-operator-manifests.yaml  --validate=false
   namespace/cass-operator created
   serviceaccount/cass-operator created
   secret/cass-operator-webhook-config created
   customresourcedefinition.apiextensions.k8s.io/cassandradatacenters.cassandra.datastax.com created
   clusterrole.rbac.authorization.k8s.io/cass-operator-cluster-role created
   clusterrolebinding.rbac.authorization.k8s.io/cass-operator created
   role.rbac.authorization.k8s.io/cass-operator created
   rolebinding.rbac.authorization.k8s.io/cass-operator created
   service/cassandradatacenter-webhook-service created
   deployment.apps/cass-operator created
   validatingwebhookconfiguration.admissionregistration.k8s.io/cassandradatacenter-webhook-registration created

This command will create the following:

:namespace: Creation of the namespace `cass-operator`
:ServiceAccount: Creation of the service account `cass-operator` in the namespace `cass-operator`
:Role: Creation of the role `cass-operator` in the namespace `cass-operator`
:RoleBinding: Bind the role `cass-operator` in the namespace `cass-operator` to service account `cass-operator`
:Resources: CassandraDatacenter interface
:Deployment: define deployment for the cass-operator docker

Post-requisites
---------------
* Check if the operator has deployed successfully: 

.. code-block:: shell

   $> kubectl -n cass-operator get deployments
   NAME            READY   UP-TO-DATE   AVAILABLE   AGE
   cass-operator   1/1     1            1           2m8s

* Verify if the service account is created:

.. code-block:: shell
   :emphasize-lines: 3

   $> kubectl get serviceaccounts --namespace=cass-operator
   NAME            SECRETS   AGE
   cass-operator   1         9m57s
   default         1         9m57s

* Verify if cass-operator main pod is created:   

.. code-block:: shell
   :emphasize-lines: 3

   $> kubectl get pods --namespace=cass-operator
   NAME                             READY   STATUS    RESTARTS   AGE
   cass-operator-65cf9cf944-vg9bb   1/1     Running   0          3m16s

* Verify if all services have been created:  

.. code-block:: shell
   :emphasize-lines: 3, 4

   $> kubectl get svc --namespace=cass-operator
   NAME                    TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)             AGE
   cass-operator-metrics   ClusterIP   10.51.253.196   <none>        8383/TCP,8686/TCP   42s
   cassandradatacenter-webhook-service   ClusterIP   10.51.240.144   <none>        443/TCP             2m37s
   
* To check the metrics pagelm execute the below command and open the browser on http://localhost:8383/metrics   

.. code-block:: shell

   $> kubectl port-forward -n cass-operator svc/cass-operator-metrics 8383:8383

* To list all clusters managed by this operator:

.. code-block:: shell

   $> kubectl -n cass-operator get cassdcs -o wide   
   No resources found.


