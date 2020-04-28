Install operator
================

.. note::
   Refer to DataStax main page https://github.com/datastax/dse-metric-reporter-dashboards for more information

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`../../dse/install/create-datacenter`
* :doc:`../operatorhub/operator`

Procedure
---------
* Install the Grafana Operator:   

.. code-block:: shell
   :emphasize-lines: 2, 3, 4


   $> kubectl create -f k8s-build/generated/grafana/operator.yaml 
   namespace/grafana-operator created
   operatorgroup.operators.coreos.com/operatorgroup created
   subscription.operators.coreos.com/grafana-operator created

Post-requisites
---------------
* Check if operator was created:

.. code-block:: shell
   :emphasize-lines: 8

   $> kubectl get pods --namespace=cass-operator
   NAME                                   READY   STATUS    RESTARTS   AGE
   cass-operator-8646fbbc5d-wcb44         1/1     Running   0          42m
   cluster1-dc1-rack1-sts-0               2/2     Running   0          38m
   cluster1-dc1-rack2-sts-0               2/2     Running   0          38m
   cluster1-dc1-rack3-sts-0               2/2     Running   0          38m
   grafana-operator-57f8c4f67-s8s54       1/1     Running   0          21s
   prometheus-operator-7df548ccd6-dv7mg   1/1     Running   0          14m
   prometheus-prometheus-k8s-0            3/3     Running   1          7m35s
