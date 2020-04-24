Install Grafana operator
========================

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

   $> kubectl create -f k8s-build/generated/grafana/operator.yaml 
   namespace/grafana-operator created
   operatorgroup.operators.coreos.com/operatorgroup created
   subscription.operators.coreos.com/grafana-operator created

Post-requisites
---------------
