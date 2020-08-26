Cloud Load balancer
===================

.. note::
   This is in addition to all notes available on DataStax https://github.com/datastax/management-api-for-apache-cassandra

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`../install/create-datacenter`

Procedure
---------
* If you are working in the cloud, the kubernetes engine of the cloud provider shall provide LB capabiliites and xpose the port management API on the network:

.. code-block:: shell
   :emphasize-lines: 2

   $> kubectl expose service cluster1-dc1-service --type=LoadBalancer -n cass-operator --name=lb
   service/lb exposed


Post-requisites
---------------
* Verify if the LB is active and retrieve it's IP:

.. code-block:: shell
   :emphasize-lines: 8

   $> kubectl get svc -n cass-operator -o wide
   NAME                                  TYPE           CLUSTER-IP      EXTERNAL-IP     PORT(S)                         AGE   SELECTOR
   cass-operator-metrics                 ClusterIP      10.51.248.158   <none>          8383/TCP,8686/TCP               22h   name=cass-operator
   cassandradatacenter-webhook-service   ClusterIP      10.51.253.92    <none>          443/TCP                         22h   name=cass-operator
   cluster1-dc1-all-pods-service         ClusterIP      None            <none>          <none>                          21h   app.kubernetes.io/managed-by=cassandra-operator,cassandra.datastax.com/cluster=cluster1,cassandra.datastax.com/datacenter=dc1
   cluster1-dc1-service                  ClusterIP      None            <none>          9042/TCP,8080/TCP               21h   app.kubernetes.io/managed-by=cassandra-operator,cassandra.datastax.com/cluster=cluster1,cassandra.datastax.com/datacenter=dc1
   cluster1-seed-service                 ClusterIP      None            <none>          <none>                          21h   cassandra.datastax.com/cluster=cluster1,cassandra.datastax.com/seed-node=true
   lb                                    LoadBalancer   10.51.248.165   34.83.250.112   9042:32703/TCP,8080:30340/TCP   12m   app.kubernetes.io/managed-by=cassandra-operator,cassandra.datastax.com/cluster=cluster1,cassandra.datastax.com/datacenter=dc1

.. note::
   Once the LB is available, both port 9042 (CQL) and 8080 (HTTP management APIs) are active. 


* To remove the load balancer, simply execute the command: 

.. code-block:: shell
   :emphasize-lines: 2

   $> kubectl delete svc lb -n cass-operator
   service "lb" deleted


