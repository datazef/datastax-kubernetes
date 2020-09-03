Install Operator
================

.. note::
   Refer to DataStax main page https://github.com/datastax/dse-metric-reporter-dashboards for more information

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`../../dse/provision/create-datacenter`
* :doc:`../operatorhub/operator`

Procedure
---------

* Clone the repository https://github.com/datastax/dse-metric-reporter-dashboards
* Install the Prometheus Operator:

.. code-block:: shell

   $> kubectl create -f k8s-build/generated/prometheus/operator.yaml 
   operatorgroup.operators.coreos.com/operator-group created
   subscription.operators.coreos.com/prometheus created

The Operator ensures at all times that for each Prometheus resource in the cluster a set of Prometheus servers with the desired configuration are running. This entails aspects like the data retention time, persistent volume claims, number of replicas, the Prometheus version, and Alertmanager instances to send alerts to. Each Prometheus instance is paired with a respective configuration that specifies which monitoring targets to scrape for metrics and with which parameters.

Post-requisites
---------------
* Check if operator was created:

.. code-block:: shell
   :emphasize-lines: 7

   $> kubectl get pods --namespace=cass-operator
   NAME                                   READY   STATUS    RESTARTS   AGE
   cass-operator-8646fbbc5d-nb8pd         1/1     Running   0          23m
   cluster1-dc1-default-sts-0             2/2     Running   0          18m
   cluster1-dc1-default-sts-1             2/2     Running   0          18m
   cluster1-dc1-default-sts-2             2/2     Running   0          18m
   prometheus-operator-7df548ccd6-ldh96   1/1     Running   0          10m
   

