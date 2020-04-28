Launch instance
===============

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
   :emphasize-lines: 8, 9

   $> kubectl get svc --namespace=cass-operator
   NAME                                  TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)             AGE
   cass-operator-metrics                 ClusterIP   10.51.240.254   <none>        8383/TCP,8686/TCP   53m
   cassandradatacenter-webhook-service   ClusterIP   10.51.247.142   <none>        443/TCP             53m
   cluster1-dc1-all-pods-service         ClusterIP   None            <none>        <none>              49m
   cluster1-dc1-service                  ClusterIP   None            <none>        9042/TCP,8080/TCP   49m
   cluster1-seed-service                 ClusterIP   None            <none>        <none>              49m
   grafana-operator-metrics              ClusterIP   10.51.244.178   <none>        8080/TCP            10m
   grafana-service                       ClusterIP   10.51.249.247   <none>        3000/TCP            5s
   prometheus-operated                   ClusterIP   None            <none>        9090/TCP            18m

* To access grafana UI:   

   $> kubectl port-forward -n cass-operator svc/grafana-service 3000:3000

* To check if prometheus datasource is configured go to page: http://localhost:3000/datasources

* If you do not see the dasboards, you can import them manually: 

   * https://raw.githubusercontent.com/datastax/dse-metric-reporter-dashboards/master/grafana/dashboards/dse-analytics.json
   * https://raw.githubusercontent.com/datastax/dse-metric-reporter-dashboards/master/grafana/dashboards/system-metrics.json
   * https://raw.githubusercontent.com/datastax/dse-metric-reporter-dashboards/master/grafana/dashboards/prometheus-metrics.json
   * https://raw.githubusercontent.com/datastax/dse-metric-reporter-dashboards/master/grafana/dashboards/dse-cluster-metrics.json
   * https://raw.githubusercontent.com/datastax/dse-metric-reporter-dashboards/master/grafana/dashboards/dse-cluster-condensed.json
   * https://raw.githubusercontent.com/datastax/dse-metric-reporter-dashboards/master/grafana/dashboards/dse-search-cluster.json

