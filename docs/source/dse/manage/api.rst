Management API
==============

.. note::
   This is in addition to all notes available on DataStax https://github.com/datastax/management-api-for-apache-cassandra

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`../network/lb`

Procedure
---------
.. note:: 
   For a complete list of all endpoints, please refer to the page: https://redocly.github.io/redoc/?url=https://raw.githubusercontent.com/datastax/management-api-for-apache-cassandra/master/management-api-server/doc/openapi.json&nocors#operation/createRole

* To retrieve the list of endpoints:

.. code-block:: shell

   $> http -v GET 'http://34.83.250.112:8080/api/v0/metadata/endpoints'   
   {
            "DC": "dc1",
            "DSE_GOSSIP_STATE": "{\"dse_version\":\"6.8.0\",\"graph\":false,\"workloads\":\"Cassandra\",\"server_id\":\"E2-0A-EF-7D-8D-AC\",\"workload\":\"Cassandra\",\"active\":\"true\",\"health\":1.0}",
            "ENDPOINT_IP": "10.48.4.3",
            "HOST_ID": "ade3cd53-f071-4921-94c7-b5712cdbc6e5",
            "INTERNAL_IP": "10.48.4.3",
            "IS_ALIVE": "true",
            "JMX_PORT": "7199",
            "LOAD": "200846.0",
            "NATIVE_TRANSPORT_ADDRESS": "10.48.4.3",
            "NATIVE_TRANSPORT_PORT": "9042",
            "NATIVE_TRANSPORT_PORT_SSL": "9042",
            "NATIVE_TRANSPORT_READY": "true",
            "NET_VERSION": "768",
            "RACK": "rack3",
            "RELEASE_VERSION": "4.0.0.680",
            "SCHEMA": "70fbaabf-aa9b-373e-a6b7-61ea8992029f",
            "SCHEMA_COMPATIBILITY_VERSION": "2",
            "STATUS": "NORMAL,-4217131631407040803",
            "STORAGE_PORT": "7000",
            "STORAGE_PORT_SSL": "7001",
            "TOKENS": "\u0000\u0000\u0000\bÅy½\u001fâëvÝ\u0000\u0000\u0000\ba\u0006\u0000^zzhÁ\u0000\u0000\u0000\b\u001eD4DË\u0017\u0000\u0000\u0000\bZ¯¼¢\u0010\u0000\u0000\u0000\bú95Yñ\r\u001b\u0000\u0000\u0000\bF)\u001bWté¬\u0000\u0000\u0000\u0000\báÓ¨©{µ\u0000\u0000\u0000\bä(`¢¶Ä\u0000\u0000\u0000\u0000"
    },

Post-requisites
---------------
 


