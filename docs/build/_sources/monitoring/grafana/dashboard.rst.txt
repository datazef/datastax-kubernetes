Configure data source & dashboards
==================================

.. note::
   Refer to DataStax main page https://github.com/datastax/dse-metric-reporter-dashboards for more information

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`./operator`

Procedure
---------
* Configure and install the GrafanaDataSource:  

.. code-block:: shell
   :emphasize-lines: 2

   $> kubectl apply -f k8s-build/generated/grafana/datasource.yaml 
   grafanadatasource.integreatly.org/prometheus-grafanadatasource created

* Configure and install the GrafanaDashboard:  

.. code-block:: shell
   :emphasize-lines: 2, 3, 4, 5, 6, 7

   $> find k8s-build/generated/grafana/ -name "*.dashboard.yaml" -exec kubectl apply -f {} \;
   grafanadashboard.integreatly.org/prometheus-metrics created
   grafanadashboard.integreatly.org/dse-search-cluster created
   grafanadashboard.integreatly.org/dse-analytics created
   grafanadashboard.integreatly.org/system-metrics created
   grafanadashboard.integreatly.org/dse-cluster-metrics created
   grafanadashboard.integreatly.org/dse-cluster-condensed created

Post-requisites
---------------
