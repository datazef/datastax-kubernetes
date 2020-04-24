Launch Grafana instance
=======================

.. note::
   Refer to DataStax main page https://github.com/datastax/dse-metric-reporter-dashboards for more information

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`./operator`
* :doc:`./dashboard`

Procedure
---------
* Configure and install the Grafana deployment

.. code-block:: shell

   $> kubectl apply -f k8s-build/generated/grafana/instance.yaml 
   grafana.integreatly.org/default created


Post-requisites
---------------
* Check access with a port forward on your computer:   

.. code-block:: shell

   kubectl port-forward $(kubectl get pod --selector="name=grafana-operator" --output jsonpath='{.items[0].metadata.name}') 8080:8080
