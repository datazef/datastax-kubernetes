Cassandra datacenter config 
===========================

.. note::
   This is in addition to all notes available on DataStax https://github.com/datastax/cass-operator

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* GKE: :doc:`../../cloud/gcp/create-cluster` and :doc:`../../cloud/gcp/connect-cluster`
* :doc:`../setup/install-cass-operator`
* :doc:`../setup/install-custom-storage`

Procedure
---------
* Configure the IP address of the pods:

.. code-block:: shell

   podTemplateSpec:
    spec:
      initContainers:
      - command:
        - sh
        - -c
        - 'sed -ib -E "s/listen_address: .*/listen_address: 1.2.3.4/" /config/cassandra.yaml'
        image: busybox
        name: example
        volumeMounts:
        - mountPath: /config
          name: server-config

* To enable search, add this in the datacenter definition file under the additional-jvm-opts section:

.. code-block:: shell

        # Enable search
        - "-Dsearch-service=true"
        - "-Dcatalina.home=/opt/dse/tomcat"
        - "-Dcatalina.base=/opt/dse/tomcat"
        - "-Djava.util.logging.config.file=/opt/dse/tomcat/conf/logging.properties"
        - "-Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager"
        - "-Dtomcat.logs=/var/log/tomcat"
        - "-Dsolr.solr.home=solr/"
        - "-Ddisable.configEdit=true"

* To enable graph, add this in the datacenter definition file under the additional-jvm-opts section:

.. code-block:: shell

        # Enable graph
        - "-Dgraph-enabled=true"

* To configure the certificates, add this undeer the cassandra-yaml block:

.. code-block:: shell

      server_encryption_options:
        internode_encryption: all
        keystore: /etc/encryption/node-keystore.jks
        keystore_password: dc1
        truststore: /etc/encryption

.. note::
   By default the certificates are mounted using secrets. If ou need to modify the certificates, you need to change the secrets. Refer. to the SSL sections as needed. 
   
* Use portworx for the storage layer:

.. code-block:: shell

   podTemplateSpec:
    spec:
      schedulerName: stork
      containers:
        - args: ["/bin/sh", "-c", "tail -n+1 -F /var/log/cassandra/system.log"]
          image: busybox
          imagePullPolicy: "Always"
          name: "another-tailing-logger"
          terminationMessagePath: "/dev/termination-log"
          terminationMessagePolicy: "File"
          volumeMounts:
            - mountPath: "/var/log/cassandra"
              name: "server-logs"          


Post-requisites
---------------
