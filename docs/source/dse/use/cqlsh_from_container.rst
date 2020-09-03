cqlsh from container
====================

.. note::
   This is in addition to all notes available on DataStax https://docs.datastax.com/en/cass-operator/doc/cass-operator/cassOperatorTOC.html and to the information available https://github.com/datastax/cass-operator

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* GKE: :doc:`../../cloud/gcp/create-cluster` and :doc:`../../cloud/gcp/connect-cluster`
* :doc:`../manage/credentials`

Procedure
---------
* cqlsh into one of the nodes: 

.. code-block:: shell
   :emphasize-lines: 5

   $> kubectl -n cass-operator exec -it -c cassandra cluster1-dc1-default-sts-0 -- cqlsh -u cluster1-superuser -p '26JP5Kf50cFEWcgXpQXKPxqTSn0k1hIikH5Na9S7rlSunyF2EjBqYA'
   Connected to cluster1 at 127.0.0.1:9042.
   [cqlsh 5.0.1 | Cassandra 3.11.6 | CQL spec 3.4.4 | Native protocol v4]
   Use HELP for help.
   cluster1-superuser@cqlsh> 

Post-requisites
---------------