Install custom storage 
======================

.. note::
   This is in addition to all notes available on DataStax https://docs.datastax.com/en/cass-operator/doc/cass-operator/cassOperatorTOC.html and to the information available https://github.com/datastax/cass-operator

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* :doc:`./install-cass-operator`

Procedure
---------
* Storage class. 

.. code-block:: shell

   apiVersion: storage.k8s.io/v1
   kind: StorageClass
   metadata:
     name: server-storage
   provisioner: kubernetes.io/gce-pd
   parameters:
     type: pd-ssd
     replication-type: none
   volumeBindingMode: WaitForFirstConsumer
   reclaimPolicy: Delete

.. note::
   * reclaimPolicy: Delete => If you do not want to storage to be deleted at the same time as the pod, you can set the option reclaimPolicy to Retain to avoid the data to be deleted. 

.. warning::
   * volumeBindingMode: WaitForFirstConsumer => the default value is Immediate and should not be used. It can prevent Cassandra pods from being scheduled on a worker node. If a pod fails to run and its status reports a message like, had volume node affinity conflict, then check the volumeBindingMode of the StorageClass being used. See Topology-Aware Volume Provisioning in Kubernetes for more details.

* Create the optimized storage class (GCP):

.. code-block:: shell
   :emphasize-lines: 2

   $> kubectl create -f k8s-build/templates/cassandra/storage-gcp.yaml
   storageclass.storage.k8s.io/server-storage created

* Create the optimized storage class (AWS):

.. code-block:: shell
   :emphasize-lines: 2

   $> kubectl create -f k8s-build/templates/cassandra/storage-aws.yaml
   storageclass.storage.k8s.io/server-storage created

.. note::
   If you want to install the same setup with portworx to operate the data layer you can. use the k8s-build/templates/cassandra/portworx.yaml configuration file. 

Post-requisites
---------------
* Check if all resources are created:

.. code-block:: shell
   :emphasize-lines: 3

   $> kubectl -n cass-operator get sc
   NAME                 PROVISIONER            AGE
   server-storage       kubernetes.io/gce-pd   101s
   standard (default)   kubernetes.io/gce-pd   81m