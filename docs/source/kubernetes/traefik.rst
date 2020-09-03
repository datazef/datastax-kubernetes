Setup Traefik proxy
===================

.. note::
   This is in addition to all notes available on DataStax at https://github.com/datastax/cass-operator/tree/proxy-config/docs/proxy

Pre-requisites
--------------
Before you start, make sure you have performed the following tasks:

* Helm: :doc:`../../kubernetes/helm`

Procedure
---------
* Install Traefik helm:

.. code-block:: shell

   $> helm repo add traefik https://containous.github.io/traefik-helm-chart
   "traefik" has been added to your repositories

* Update repository

.. code-block:: shell

   $> helm repo update

* Install traefik:

.. code-block:: shell

   $> helm install traefik traefik/traefik

* Setup Traefik: 

.. code-block:: shell

   $> kubectl create -f k8s-build/templates/traefik/clusterrole.yaml
   $> kubectl create -f k8s-build/templates/traefik/customresourcedefinition.yaml

* To have access to the traefik dashboard, we need to edit the configuration file for the service:

.. code-block:: shell

   $> kubectl edit svc traefik

* Modify the ports section and add the following, leaving the nodePort configuraiton empty:

.. code-block:: shell

   - name: dashboard
      port: 9000
      protocol: TCP
      targetPort: 9000

* Delete the pod to force a restart:

.. code-block:: shell

   $> kubectl delete pod -n default -l app.kubernetes.io/instance=traefik

Post-requisites
---------------
* Check if the service is listening to port 9000 for the dashboard access:

.. code-block:: shell

   $> kubectl describe svc traefik
   Name:                     traefik
   Namespace:                default
   Labels:                   app.kubernetes.io/instance=traefik
                             app.kubernetes.io/managed-by=Helm
                             app.kubernetes.io/name=traefik
                             helm.sh/chart=traefik-8.7.0
   Annotations:              meta.helm.sh/release-name: traefik
                             meta.helm.sh/release-namespace: default
   Selector:                 app.kubernetes.io/instance=traefik,app.kubernetes.io/name=traefik
   Type:                     LoadBalancer
   IP:                       10.55.254.57
   LoadBalancer Ingress:     35.233.233.245
   Port:                     web  80/TCP
   TargetPort:               web/TCP
   NodePort:                 web  30558/TCP
   Endpoints:                10.52.2.2:8000
   Port:                     websecure  443/TCP
   TargetPort:               websecure/TCP
   NodePort:                 websecure  31499/TCP
   Endpoints:                10.52.2.2:8443
   Port:                     dashboard  9000/TCP
   TargetPort:               9000/TCP
   NodePort:                 dashboard  32117/TCP
   Endpoints:                10.52.2.2:9000
   Port:                     cassandra-tls  9142/TCP
   TargetPort:               9142/TCP
   NodePort:                 cassandra-tls  30014/TCP
   Endpoints:                10.52.2.2:9142
   Session Affinity:         None
   External Traffic Policy:  Cluster
   Events:
     Type    Reason                Age                From                Message
     ----    ------                ----               ----                -------
     Normal  EnsuringLoadBalancer  22m (x3 over 42m)  service-controller  Ensuring load balancer
     Normal  EnsuredLoadBalancer   21m (x3 over 41m)  service-controller  Ensured load balancer

* Acccess the traefik web portal (use command kubectl get svc to get the external IP) using the URL http://<EXTERNAL-IP>:9000/dashbaord/

* Check the pod to ensure it has the proper args if you need to further troubleshoot:

.. code-block:: shell

   $> kubectl describe pod traefik-54d7ff7cb9-ws2n5

