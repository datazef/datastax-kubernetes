Install Datastax Studio
=======================

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* GKE: :doc:`../../cloud/gcp/create-cluster` and :doc:`../../cloud/gcp/connect-cluster`

Procedure
---------
* Install DataStax studio with the following deployment:

.. code-block:: shell

   $> kubectl -n cass-operator create -f k8s-build/templates/datastax/studio.yaml 

.. warning::
   Be careful to install the adequate version. Refer to the studio.yaml and changed as needed.

Post-requisites
---------------
* Check if the studio pod is properly started:

.. code-block:: shell
   :emphasize-lines: 7

   $> kubectl -n cass-operator get pods
   NAME                             READY   STATUS    RESTARTS   AGE
   cass-operator-68568d98fd-l6w4r   1/1     Running   0          3m32s
   cluster1-dc1-rack1-sts-0         1/2     Running   0          2m3s
   cluster1-dc1-rack2-sts-0         1/2     Running   0          2m3s
   cluster1-dc1-rack3-sts-0         1/2     Running   0          2m3s
   studio-d6d695d8-qr45r            1/1     Running   0          94s

* Connect to the service via the load balancer:

.. code-block:: shell
   :emphasize-lines: 8

   $> kubectl -n cass-operator get svc
   NAME                                  TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)                      AGE
   cass-operator-metrics                 ClusterIP      10.51.244.139   <none>        8383/TCP,8686/TCP            4m39s
   cassandradatacenter-webhook-service   ClusterIP      10.51.253.97    <none>        443/TCP                      4m48s
   cluster1-dc1-all-pods-service         ClusterIP      None            <none>        9042/TCP,8080/TCP,9103/TCP   3m23s
   cluster1-dc1-service                  ClusterIP      None            <none>        9042/TCP,8080/TCP,9103/TCP   3m23s
   cluster1-seed-service                 ClusterIP      None            <none>        <none>                       3m23s
   studio                                LoadBalancer   10.51.252.49    34.82.65.57   9091:31515/TCP               2m50s