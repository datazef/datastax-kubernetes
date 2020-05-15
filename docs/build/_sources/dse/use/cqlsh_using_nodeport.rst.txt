cqlsh using NodePort service
============================

.. note::
   This is in addition to all notes available on DataStax https://docs.datastax.com/en/cass-operator/doc/cass-operator/cassOperatorTOC.html and to the information available https://github.com/datastax/cass-operator

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* GKE: :doc:`../../cloud/gcp/create-cluster` and :doc:`../../cloud/gcp/connect-cluster`
* :doc:`credentials`

Procedure
---------
* Retrieve the list of public IPs for the cluster: 

.. code-block:: shell

   $> kubectl get nodes -o wide
   
   NAME                                         STATUS   ROLES    AGE   VERSION           INTERNAL-IP   EXTERNAL-IP     OS-IMAGE                             KERNEL-VERSION   CONTAINER-RUNTIME
   gke-cluster-dse-default-pool-5833fc98-lcct   Ready    <none>   24h   v1.14.10-gke.27   10.138.0.3    35.247.39.114   Container-Optimized OS from Google   4.14.138+        docker://18.9.7
   gke-cluster-dse-default-pool-5833fc98-vl15   Ready    <none>   24h   v1.14.10-gke.27   10.138.0.4    34.105.4.104    Container-Optimized OS from Google   4.14.138+        docker://18.9.7
   gke-cluster-dse-default-pool-6aae0f91-c6hv   Ready    <none>   24h   v1.14.10-gke.27   10.138.0.7    34.105.19.166   Container-Optimized OS from Google   4.14.138+        docker://18.9.7
   gke-cluster-dse-default-pool-6aae0f91-n4pw   Ready    <none>   24h   v1.14.10-gke.27   10.138.0.5    34.105.76.136   Container-Optimized OS from Google   4.14.138+        docker://18.9.7
   gke-cluster-dse-default-pool-8d04372a-psc3   Ready    <none>   24h   v1.14.10-gke.27   10.138.0.10   34.83.51.0      Container-Optimized OS from Google   4.14.138+        docker://18.9.7
   gke-cluster-dse-default-pool-8d04372a-sg5k   Ready    <none>   24h   v1.14.10-gke.27   10.138.0.11   35.197.37.114   Container-Optimized OS from Google   4.14.138+        docker://18.9.7
   

* Expose pod with a service of type NodePort: 

.. code-block:: shell

   $> kubectl expose pod cluster1-dc1-rack1-sts-0 --type=NodePort --name=nodeport -n cass-operator

* Retrieve the port number used for this NodePort service:

.. code-block:: shell
   :emphasize-lines: 6

   $> kubectl describe svc nodeport -n cass-operator 
   Type:                     NodePort
   IP:                       10.51.252.107
   Port:                     port-1  9042/TCP
   TargetPort:               9042/TCP
   NodePort:                 port-1  32564/TCP  

* Connect to DSE uwing the public IP and the port: 

.. code-block:: shell
   :emphasize-lines: 5

   $> ./cqlsh -u cluster1-superuser -p't6X6bk6zfrf7O-10AUCC7z2ksuurE1-FncTa4al_-H4AlWx1bYUsZA' 35.247.39.114 32564
   Connected to cluster1 at 127.0.0.1:9042.
   [cqlsh 5.0.1 | Cassandra 3.11.6 | CQL spec 3.4.4 | Native protocol v4]
   Use HELP for help.
   cluster1-superuser@cqlsh> 

.. warning::
   When using DSE via a load balancer provided by the cloud the mapping of the private IPs of the pods advertised via GOSSIP is not correct. User is required to user a WhiteListPolicy to only use the LB as a contact point.

Post-requisites
---------------
