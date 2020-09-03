Portworx 
========

Create deployment
-----------------

* Signup and create a deployment using portworx portal: https://central.portworx.com/
* Once deployment is created, launch it using the provided command on the portal

.. code-block:: shell
   
   $> kubectl apply -f 'https://install.portworx.com/2.5?mc=false&kbver=1.15.12-gke.2&b=true&s=%22type%3Dpd-ssd%2Csize%3D150%22&kd=type%3Dpd-standard%2Csize%3D150&c=px-cluster-73f06a39-cf6d-44d9-a31f-4066f07fbf1c&gke=true&stork=true&st=k8s'
   
Get master
----------

* Retrieve the portworx master 

.. code-block:: shell

   $> PX_POD=$(kubectl get pods -l name=portworx -n kube-system -o jsonpath='{.items[0].metadata.name}')

Get status
----------

* Get the status of the portworx system

.. code-block:: shell

   $> kubectl exec $PX_POD -n kube-system -- /opt/pwx/bin/pxctl status


List volumes
------------

* List volumes:

.. code-block:: shell

   $> kubectl exec $PX_POD -n kube-system -- /opt/pwx/bin/pxctl volume list
   ID      NAME            SIZE  HA  SHARED  ENCRYPTED IO_PRIORITY STATUS        SNAP-ENABLED  
   542415959732180030  pvc-59581bb7-2826-4228-bfbd-1540d753ca01  10 GiB  2 no  no    HIGH    up - attached on 10.138.15.225  no
   125897915673776583  pvc-5a0e110a-8d7d-43c8-8768-f78b071ee7a7  10 GiB  2 no  no    HIGH    up - attached on 10.138.15.220  no
   492744781622959243  pvc-c6381f94-96da-4745-9a97-ba6b837b6980  10 GiB  2 no  no    HIGH    up - attached on 10.138.15.223  no

Inspect volume
---------------

* Inspect volumes:

.. code-block:: shell

   $> kubectl exec $PX_POD -n kube-system -- /opt/pwx/bin/pxctl volume inspect 492744781622959243