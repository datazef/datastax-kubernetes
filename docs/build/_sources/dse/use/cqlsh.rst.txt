cqlsh into a k8s cassandra cluster 
==================================

.. note::
   This is in addition to all notes available on DataStax https://docs.datastax.com/en/cass-operator/doc/cass-operator/cassOperatorTOC.html and to the information available https://github.com/datastax/cass-operator

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* GKE: :doc:`../../cloud/gcp/create-cluster` and :doc:`../../cloud/gcp/connect-cluster`

Procedure
---------
* Retrieve the user to retrieve secrets for:

.. code-block:: shell
   :emphasize-lines: 2

   $> kubectl get secrets -n cass-operator | grep cluster1
   cluster1-superuser          Opaque                                2      36m

* Retrieve the secrets to retrieve login/password information:

.. code-block:: shell
   :emphasize-lines: 4, 5

   $> kubectl get secret cluster1-superuser -n cass-operator -o yaml
   apiVersion: v1
   data:
     password: MjZKUDVLZjUwY0ZFV2NnWHBRWEtQeHFUU24wazFoSWlrSDVOYTlTN3JsU3VueUYyRWpCcVlB
     username: Y2x1c3RlcjEtc3VwZXJ1c2Vy
   kind: Secret
   metadata:
     creationTimestamp: "2020-04-21T23:07:59Z"
     name: cluster1-superuser
     namespace: cass-operator
     resourceVersion: "29457"
     selfLink: /api/v1/namespaces/cass-operator/secrets/cluster1-superuser
     uid: f1b731aa-8424-11ea-b971-42010a8a00a2
   type: Opaque

* Decode the login: 

.. code-block:: shell
   :emphasize-lines: 2

   $> echo 'Y2x1c3RlcjEtc3VwZXJ1c2Vy' | base64 --decode
   cluster1-superuser

* Decode the password: 

.. code-block:: shell
   :emphasize-lines: 2

   $> echo 'MjZKUDVLZjUwY0ZFV2NnWHBRWEtQeHFUU24wazFoSWlrSDVOYTlTN3JsU3VueUYyRWpCcVlB' | base64 --decode
   26JP5Kf50cFEWcgXpQXKPxqTSn0k1hIikH5Na9S7rlSunyF2EjBqYA

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
