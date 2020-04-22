*****************
Create datacenter 
*****************

.. note::
   This is in addition to all notes available on DataStax https://docs.datastax.com/en/cass-operator/doc/cass-operator/cassOperatorTOC.html and to the information available https://github.com/datastax/cass-operator

Pre-requisites
##############
Before you start, make sure you have performed the following tasks:

* GKE: :doc:`../cloud/gcp/create-cluster` and :doc:`../cloud/gcp/connect-cluster`

Procedure
#########
* Create a datacenter with 3 nodes (one per rack):

.. code-block:: shell

   $> kubectl -n cass-operator apply -f https://raw.githubusercontent.com/datastax/cass-operator/26ad52bfc8f450852f5573fa2904a5df407ce2d3/operator/example-cassdc-yaml/cassandra-3.11.6/example-cassdc-minimal.yaml
   cassandradatacenter.cassandra.datastax.com/dc1 created

Post-requisites
###############
* Check if all resources are created:

.. code-block:: shell

   $> kubectl get pods -n cass-operator --selector cassandra.datastax.com/cluster=cluster1
   cluster1-dc1-default-sts-0   2/2     Running   0          2m2s
   cluster1-dc1-default-sts-1   1/2     Running   0          2m2s
   cluster1-dc1-default-sts-2   1/2     Running   0          2m2s

   $> kubectl -n cass-operator exec -it -c cassandra cluster1-dc1-default-sts-0 -- nodetool status
   Datacenter: dc1
   ===============
   Status=Up/Down
   |/ State=Normal/Leaving/Joining/Moving
   --  Address     Load       Tokens       Owns (effective)  Host ID                               Rack
   UN  10.48.7.5   70.19 KiB  1            43.7%             36ccd8cf-b449-4dab-9f40-512bbb68bb72  default
   UN  10.48.3.7   103.54 KiB  1            68.0%             614748cd-d799-4f8c-b0ac-55bcf6cfa049  default
   UN  10.48.12.7  84.42 KiB  1            88.2%             b992c9c4-68fd-41c7-be42-ef7fae32a5aa  default

   $> kubectl -n cass-operator get cassdc/dc1 -o "jsonpath={.status.cassandraOperatorProgress}"
   Ready