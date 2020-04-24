Install OperatorHub Lifecycle Manager 
=====================================

.. note::
   Refer to DataStax main page https://github.com/datastax/dse-metric-reporter-dashboards for more information

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`../../dse/install/create-datacenter`

Procedure
---------
* Install the OperatorHub Lifecycle Manager:

.. code-block:: shell

   $> curl -sL https://github.com/operator-framework/operator-lifecycle-manager/releases/download/0.14.1/install.sh | bash -s 0.14.1
   customresourcedefinition.apiextensions.k8s.io/clusterserviceversions.operators.coreos.com configured
   customresourcedefinition.apiextensions.k8s.io/installplans.operators.coreos.com configured
   customresourcedefinition.apiextensions.k8s.io/subscriptions.operators.coreos.com configured
   customresourcedefinition.apiextensions.k8s.io/catalogsources.operators.coreos.com configured
   customresourcedefinition.apiextensions.k8s.io/operatorgroups.operators.coreos.com configured
   namespace/olm unchanged
   namespace/operators unchanged
   serviceaccount/olm-operator-serviceaccount unchanged
   clusterrole.rbac.authorization.k8s.io/system:controller:operator-lifecycle-manager unchanged
   clusterrolebinding.rbac.authorization.k8s.io/olm-operator-binding-olm unchanged
   deployment.apps/olm-operator configured
   deployment.apps/catalog-operator configured
   clusterrole.rbac.authorization.k8s.io/aggregate-olm-edit unchanged
   clusterrole.rbac.authorization.k8s.io/aggregate-olm-view unchanged
   operatorgroup.operators.coreos.com/global-operators unchanged
   operatorgroup.operators.coreos.com/olm-operators unchanged
   clusterserviceversion.operators.coreos.com/packageserver unchanged
   catalogsource.operators.coreos.com/operatorhubio-catalog unchanged
   deployment "olm-operator" successfully rolled out
   deployment "catalog-operator" successfully rolled out
   Package server phase: Succeeded
   deployment "packageserver" successfully rolled out

.. note::
   If the script does not work, a modified version with the option --validate=false removed is available in the repo https://github.com/datazef/datastax-kubernetes/. You can run it with the command k8s-build/templates/grafana/install.sh 0.14.1

Post-requisites
---------------
* Check if all resources are created:

.. code-block:: shell

   $> kubectl get pods --namespace=olm
   NAME                                READY   STATUS    RESTARTS   AGE
   catalog-operator-66cf4f96f4-6vvfc   1/1     Running   0          10m
   olm-operator-9b64f8547-r4zfv        1/1     Running   0          10m
   operatorhubio-catalog-bfdsr         1/1     Running   0          10m
   packageserver-597999d959-5zftz      1/1     Running   0          10m
   packageserver-597999d959-pqghc      1/1     Running   0          10m
