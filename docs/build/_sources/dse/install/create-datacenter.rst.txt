Create a Cassandra cluster 
==========================

.. note::
   This is in addition to all notes available on DataStax https://docs.datastax.com/en/cass-operator/doc/cass-operator/cassOperatorTOC.html and to the information available https://github.com/datastax/cass-operator

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* GKE: :doc:`../../cloud/gcp/create-cluster` and :doc:`../../cloud/gcp/connect-cluster`
* :doc:`./install-cass-operator`
* :doc:`./install-custom-storage`

Procedure
---------
* Create a datacenter with 3 nodes (one per rack):

.. code-block:: shell

   $> kubectl -n cass-operator create -f k8s-build/templates/cassandra/example-dse-full.yaml
   cassandradatacenter.cassandra.datastax.com/dc1 created

.. warning::
   Some features are still being developed for the cassandra version. Please install DSE to see all features in action.

Post-requisites
---------------
* Check if all pods are created (topology: dc1[3 nodes]):

.. code-block:: shell
   :emphasize-lines: 2, 3, 4

   $> kubectl get pods -n cass-operator --selector cassandra.datastax.com/cluster=cluster1
   cluster1-dc1-default-sts-0   2/2     Running   0          2m2s
   cluster1-dc1-default-sts-1   1/2     Running   0          2m2s
   cluster1-dc1-default-sts-2   1/2     Running   0          2m2s


* Once all pods are up and running, you can check the status of the cassandra cluster:

.. code-block:: shell
   :emphasize-lines: 7, 8, 9

   $> kubectl -n cass-operator exec -it -c cassandra cluster1-dc1-rack1-sts-0 -- nodetool status
   Datacenter: dc1
   ===============
   Status=Up/Down
   |/ State=Normal/Leaving/Joining/Moving
   --  Address     Load       Tokens       Owns (effective)  Host ID                               Rack
   UN  10.48.7.5   70.19 KiB  1            43.7%             36ccd8cf-b449-4dab-9f40-512bbb68bb72  default
   UN  10.48.3.7   103.54 KiB  1            68.0%             614748cd-d799-4f8c-b0ac-55bcf6cfa049  default
   UN  10.48.12.7  84.42 KiB  1            88.2%             b992c9c4-68fd-41c7-be42-ef7fae32a5aa  default

* Or get the Operator progress report:

.. code-block:: shell
   :emphasize-lines: 2

   $> kubectl -n cass-operator get cassdc/dc1 -o "jsonpath={.status.cassandraOperatorProgress}"
   Ready

* DC service endpoints:

.. code-block:: shell
   :emphasize-lines: 13

   $> kubectl describe svc cluster1-dc1-service -n cass-operator 
   Name:              cluster1-dc1-service
   Namespace:         cass-operator
   Labels:            app.kubernetes.io/managed-by=cassandra-operator
                      cassandra.datastax.com/cluster=cluster1
                      cassandra.datastax.com/datacenter=dc1
   Annotations:       <none>
   Selector:          app.kubernetes.io/managed-by=cassandra-operator,cassandra.datastax.com/cluster=cluster1,cassandra.datastax.com/datacenter=dc1
   Type:              ClusterIP
   IP:                None
   Port:              native  9042/TCP
   TargetPort:        9042/TCP
   Endpoints:         10.48.3.3:9042,10.48.4.3:9042,10.48.5.3:9042
   Port:              mgmt-api  8080/TCP
   TargetPort:        8080/TCP
   Endpoints:         10.48.3.3:8080,10.48.4.3:8080,10.48.5.3:8080
   Session Affinity:  None
   Events:            <none>

