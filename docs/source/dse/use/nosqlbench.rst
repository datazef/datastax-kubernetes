Launch a nosqlbench load test
=============================

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* GKE: :doc:`../../cloud/gcp/create-cluster` and :doc:`../../cloud/gcp/connect-cluster`
* :doc:`../setup/install-cass-operator`
* :doc:`../provision/create-datacenter`
* :doc:`../setup/studio`
* :doc:`../manage/credentials`

Procedure
---------
* Below a job configuration example on how to launch a job in kubernetes:

.. code-block:: shell

   apiVersion: batch/v1
   kind: Job
   metadata:
     name: nosqlbench
     namespace: cass-operator
   spec:
     ttlSecondsAfterFinished: 0
     completions: 1
     parallelism: 1
     template:
       spec:
         containers:
         - name: nosqlbench
           image: nosqlbench/nosqlbench
           command: ["java","-jar", "nb.jar", "activities/baselines/cql-keyvalue", "default", "hosts=cluster1-dc1-service", "username=cluster1-superuser", "password=Qi4PgzWZg1fXhpzT_HNQ11H2dkMok7-KpVY9JoiN__fDLwBKqKuu4w", "pooling=8:8:32000", "threads=auto", "--report-csv-to=metrics", "cyclerate=20000", "async=20000"]
         restartPolicy: Never
     backoffLimit: 0

* To launch the load simulation:

.. code-block:: shell

   $> kubectl create -f k8s-build/templates/datastax/nosqlbench.yaml

* Monitor metrics from nosqlbench while test run:

.. code-block:: shell

   $> kubectl exec -it -n cass-operator nosqlbench-lwbmw /bin/ash

.. note::
   The above job configuration will create a folder metrics inside the container will all the metrics generated. If you want to only retrieve p99 for a specific metric, you use use the command cat XXX.csv | cut -d',' -f11     

Post-requisites
---------------
* Remove nosqlbench pod once job is completed:

.. code-block:: shell

   $> kubectl create -f kubectl delete jobs nosqlbench -n cass-operator