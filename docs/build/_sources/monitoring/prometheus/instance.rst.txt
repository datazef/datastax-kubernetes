Launch Instance
===============

.. note::
   Refer to DataStax main page https://github.com/datastax/dse-metric-reporter-dashboards for more information

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`./service`

Procedure
---------
* Edit the file k8s-build/generated/prometheus/instance.yaml to match the configuration, i.e:

.. code-block:: shell

   spec:
     replicas: 1
     serviceAccountName: prometheus
     securityContext: {}
     serviceMonitorSelector:
       matchLabels:
         cassandra.datastax.com/cluster: cluster1

 * Create prometheus instance:        

.. code-block:: shell
   :emphasize-lines: 2, 3, 4, 5

   $> kubectl apply -f k8s-build/generated/prometheus/instance.yaml
   serviceaccount/prometheus created
   clusterrole.rbac.authorization.k8s.io/prometheus created
   clusterrolebinding.rbac.authorization.k8s.io/prometheus created
   prometheus.monitoring.coreos.com/default created


Post-requisites
---------------
* Check if the web portal is open

.. code-block:: shell

   $> kubectl port-forward -n cass-operator svc/prometheus-operated 9090:9090

* To check if data gets collected, you can try this page: http://localhost:9090/graph?g0.range_input=1h&g0.expr=collectd_disk_disk_ops_read_total&g0.tab=1   

* To verify the final state you should have one service and one pod:

.. code-block:: shell
   :emphasize-lines: 7, 8, 18

   $> kubectl get pods --namespace=cass-operator
   NAME                                   READY   STATUS    RESTARTS   AGE
   cass-operator-8646fbbc5d-wcb44         1/1     Running   0          42m
   cluster1-dc1-rack1-sts-0               2/2     Running   0          38m
   cluster1-dc1-rack2-sts-0               2/2     Running   0          38m
   cluster1-dc1-rack3-sts-0               2/2     Running   0          38m
   prometheus-operator-7df548ccd6-dv7mg   1/1     Running   0          14m
   prometheus-prometheus-k8s-0            3/3     Running   1          7m35s


   kubectl get svc --namespace=cass-operator
   NAME                                  TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)             AGE
   cass-operator-metrics                 ClusterIP   10.51.240.254   <none>        8383/TCP,8686/TCP   44m
   cassandradatacenter-webhook-service   ClusterIP   10.51.247.142   <none>        443/TCP             44m
   cluster1-dc1-all-pods-service         ClusterIP   None            <none>        <none>              40m
   cluster1-dc1-service                  ClusterIP   None            <none>        9042/TCP,8080/TCP   40m
   cluster1-seed-service                 ClusterIP   None            <none>        <none>              40m
   prometheus-operated                   ClusterIP   None            <none>        9090/TCP            9m21s


