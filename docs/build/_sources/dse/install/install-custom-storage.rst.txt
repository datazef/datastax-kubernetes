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
* Deploy the optimized storage class:

.. code-block:: shell
   :emphasize-lines: 2

   $> kubectl create -f k8s-build/templates/cassandra/storage.yaml
   storageclass.storage.k8s.io/server-storage created


Post-requisites
---------------
* Check if all resources are created:

.. code-block:: shell
   :emphasize-lines: 3

   $> kubectl -n cass-operator get sc
   NAME                 PROVISIONER            AGE
   server-storage       kubernetes.io/gce-pd   101s
   standard (default)   kubernetes.io/gce-pd   81m