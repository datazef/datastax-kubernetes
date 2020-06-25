Configure SSL certificates
==========================

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:


Procedure
---------
* Retrieve the list of host IDs we need to create an SSL for:

.. code-block:: shell
   :emphasize-lines: 4, 8, 12

   $> kubectl get cassdc -o json -n cass-operator | jq ".items[0].status.nodeStatuses"
   {
     "cluster1-dc1-rack1-sts-0": {
       "hostID": "b7d841bc-9f36-493d-a527-0766f00da924",
       "nodeIP": "10.52.0.9"
     },
     "cluster1-dc1-rack2-sts-0": {
       "hostID": "74f07959-0023-4f8e-9364-e8c87f82f32c",
       "nodeIP": "10.52.3.4"
     },
     "cluster1-dc1-rack3-sts-0": {
       "hostID": "4668427b-ed14-4a6a-abeb-d1f04f583a0d",
       "nodeIP": "10.52.1.3"
     }
   }

* Generate a certificate authority:

.. code-block:: shell

   $> cfssl gencert -initca k8s-build/templates/ssl/ca.csr.json | cfssljson -bare ca
   2020/06/24 15:18:38 [INFO] generating a new CA key and certificate from CSR
   2020/06/24 15:18:38 [INFO] generate received request
   2020/06/24 15:18:38 [INFO] received CSR
   2020/06/24 15:18:38 [INFO] generating key: rsa-2048
   2020/06/24 15:18:38 [INFO] encoded CSR
   2020/06/24 15:18:38 [INFO] signed certificate with serial number 161383111145976000625978427714444678653324159892

The previous command will generate 3 files: ca-key.pem, ca.csr, ca.pem

* Create the secret resource:

.. code-block:: shell

   $> kubectl create secret tls ca-cert --cert ca.pem --key ca-key.pem
   secret/ca-cert created

* Generate the ingress certificate:

.. code-block:: shell

   $> cfssl gencert -ca ca.pem -ca-key ca-key.pem k8s-build/templates/ssl/ingress.csr.json | cfssljson -bare 
   2020/06/24 15:27:56 [INFO] generate received request
   2020/06/24 15:27:56 [INFO] received CSR
   2020/06/24 15:27:56 [INFO] generating key: rsa-2048
   2020/06/24 15:27:56 [INFO] encoded CSR
   2020/06/24 15:27:56 [INFO] signed certificate with serial number 657659756304594244742693609782164025173023012622

The previous command will generate 3 files: ingress-key.pem, ingress.csr, ingress.pem

* Create the secret resource:

.. code-block:: shell

   $> kubectl create secret tls sample-cluster-sample-dc-cert --cert ingress.pem --key ingress-key.pem
   secret/sample-cluster-sample-dc-cert created

* Create and sign Client certificate

.. code-block:: shell

   $> cfssl gencert -ca ca.pem -ca-key ca-key.pem k8s-build/templates/ssl/client.csr.json | cfssljson -bare client
   2020/06/24 15:31:47 [INFO] generate received request
   2020/06/24 15:31:47 [INFO] received CSR
   2020/06/24 15:31:47 [INFO] generating key: rsa-2048
   2020/06/24 15:31:47 [INFO] encoded CSR
   2020/06/24 15:31:47 [INFO] signed certificate with serial number 282179691075855076969928348357272306708748688455
   2020/06/24 15:31:47 [WARNING] This certificate lacks a "hosts" field. This makes it unsuitable for websites. 

* Install TLS Options to add support for mutual TLS:

.. code-block:: shell

   $> kubectl apply -f k8s-build/templates/ssl/sample-cluster-sample-dc.tlsoption.yaml 
   tlsoption.traefik.containo.us/sample-cluster-sample-dc-options created

* Install TLS Options to add support for mutual TLS:

.. code-block:: shell

   $> kubectl apply -f k8s-build/templates/ssl/sample-cluster-sample-dc.ingressroutetcp.yaml
   ingressroutetcp.traefik.containo.us/sample-cluster-sample-dc created

Post-requisites
---------------

