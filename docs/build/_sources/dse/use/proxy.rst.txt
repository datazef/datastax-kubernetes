Setup proxy DSE/Cassandra
=========================

.. note::
   This is in addition to all notes available on DataStax https://docs.datastax.com/en/cass-operator/doc/cass-operator/cassOperatorTOC.html and to the information available https://github.com/datastax/cass-operator

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* GKE: :doc:`../../cloud/gcp/create-cluster` and :doc:`../../cloud/gcp/connect-cluster`
* :doc:`credentials`
* :doc:`../../kubernetes/proxy`

Procedure
---------
* Configure the proxy to follow traffic on port 9142. First we edit the service file and ensure it is configured to manage port 9142:

.. code-block:: shell

   $> kubectl edit svc traefik 
    - name: cassandra-tls
       port: 9142
       protocol: TCP
       targetPort: 9142

* Second, we edit the deployment to add the 9142 entry point as shown below:

.. code-block:: shell

   $> kubectl edit deployment traefik 
    - --entryPoints.cassandra-tls.address=:9142/tcp

Post-requisites
---------------

