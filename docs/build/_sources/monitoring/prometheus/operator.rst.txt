Install Prometheus Operator
===========================

.. note::
   Refer to DataStax main page https://github.com/datastax/dse-metric-reporter-dashboards for more information

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`../../dse/install/create-datacenter`
* :doc:`../operatorhub/operator`

Procedure
---------
* Clone the repository https://github.com/datastax/dse-metric-reporter-dashboards
* Install the Prometheus Operator:

.. code-block:: shell

   $> kubectl create -f k8s-build/generated/prometheus/operator.yaml 
   operatorgroup.operators.coreos.com/operator-group created
   subscription.operators.coreos.com/prometheus created

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

   kubectl get pods --namespace=cass-operator
   NAME                                   READY   STATUS    RESTARTS   AGE
   cass-operator-8646fbbc5d-nb8pd         1/1     Running   0          23m
   cluster1-dc1-default-sts-0             2/2     Running   0          18m
   cluster1-dc1-default-sts-1             2/2     Running   0          18m
   cluster1-dc1-default-sts-2             2/2     Running   0          18m
   prometheus-operator-7df548ccd6-ldh96   1/1     Running   0          10m
   
