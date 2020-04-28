Install Service
===============

.. note::
   Refer to DataStax main page https://github.com/datastax/dse-metric-reporter-dashboards for more information

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`./operator`

Procedure
---------
* Edit the file k8s-build/prometheus/service_monitor.yaml to match the configuration, i.e:

.. code-block:: shell
   :emphasize-lines: 3, 7, 12

   $> kubectl get svc --show-labels -n cass-operator
   NAME                            TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)             AGE   LABELS
   cluster1-seed-service           ClusterIP   None           <none>        <none>              18h   app.kubernetes.io/managed-by=cassandra-operator,cassandra.datastax.com/cluster=cluster1

   metadata:
     labels:
       cassandra.datastax.com/cluster: cluster1
     name: dse-cluster

   selector:
     matchLabels:
       cassandra.datastax.com/cluster: cluster1

* Install the Prometheus service:

.. code-block:: shell
   :emphasize-lines: 2
   
   $> kubectl apply -f k8s-build/generated/prometheus/service_monitor.yaml
   servicemonitor.monitoring.coreos.com/dse-cluster created

The user can either manually specify this configuration or let the Operator generate it based on the second TPR, the ServiceMonitor. The ServiceMonitor resource specifies how metrics can be retrieved from a set of services exposing them in a common way. A Prometheus resource object can dynamically include ServiceMonitor objects by their labels. The Operator configures the Prometheus instance to monitor all services covered by included ServiceMonitors and keeps this configuration synchronized with any changes happening in the cluster.

Post-requisites
---------------

