Cheatsheet 
==========

API resources:
--------------

.. code-block:: shell
   
   $> kubectl api-resources
   NAME                              SHORTNAMES       APIGROUP                       NAMESPACED   KIND 
   bindings                                                                          true         Binding
   componentstatuses                 cs                                              false        ComponentStatus
   configmaps                        cm                                              true         ConfigMap
   endpoints                         ep                                              true         Endpoints
   events                            ev                                              true         Event
   limitranges                       limits                                          true         LimitRange
   namespaces                        ns                                              false        Namespace

List resources:
---------------

.. code-block:: shell

   $> kubectl get {namespaces|pods|nodes|serviceaccounts} --namespace=cass-operator
   NAME              STATUS   AGE
   cass-operator     Active   3m4s
   default           Active   76m
   kube-node-lease   Active   76m
   kube-public       Active   76m
   kube-system       Active   76m 

   $>kubectl get secrets -n cass-operator
   NAME                        TYPE                                  DATA   AGE
   cass-operator-token-nspdm   kubernetes.io/service-account-token   3      56m
   cluster1-superuser          Opaque                                2      35m
   default-token-jmjsf         kubernetes.io/service-account-token   3      56m

Describe pod:
---------------

.. code-block:: shell

   $> kubectl describe pod cass-operator-65cf9cf944-vg9bb -n cass-operator
   Name:           cass-operator-65cf9cf944-vg9bb
   Namespace:      cass-operator
   Priority:       0
   Node:           gke-cluster-dse-default-pool-d339feaf-m54n/10.138.0.34
   Start Time:     Tue, 21 Apr 2020 15:56:10 -0700
   Labels:         name=cass-operator
                   pod-template-hash=65cf9cf944
   Annotations:    <none>
   Status:         Running
   IP:             10.48.3.6
   Controlled By:  ReplicaSet/cass-operator-65cf9cf944
   Containers:
     cass-operator:
       Container ID:   docker://f6a4d9b785ed707f0f1c3ad9de9ed76558271a03c3e1f4fbad8c20d5be9cb293
       Image:          datastax/cass-operator:1.0.0
       Image ID:       docker-pullable://datastax/cass-operator@sha256:f525e2b9279c54aac99cede8a74bb3e813db5aa89fdd39fb1b702295298c052f
       Port:           <none>
       Host Port:      <none>
       State:          Running
         Started:      Tue, 21 Apr 2020 15:56:14 -0700
       Ready:          True
       Restart Count:  0
       Liveness:       exec [pgrep .*operator] delay=5s timeout=5s period=5s #success=1 #failure=3
       Readiness:      exec [stat /tmp/operator-sdk-ready] delay=5s timeout=5s period=5s #success=1 #failure=1
       Environment:
         WATCH_NAMESPACE:          cass-operator (v1:metadata.namespace)
         POD_NAME:                 cass-operator-65cf9cf944-vg9bb (v1:metadata.name)
         OPERATOR_NAME:            cass-operator
         SKIP_VALIDATING_WEBHOOK:  TRUE
       Mounts:
         /var/run/secrets/kubernetes.io/serviceaccount from cass-operator-token-nspdm (ro)
   Conditions:
     Type              Status
     Initialized       True 
     Ready             True 
     ContainersReady   True 
     PodScheduled      True 
   Volumes:
     cass-operator-token-nspdm:
       Type:        Secret (a volume populated by a Secret)
       SecretName:  cass-operator-token-nspdm
       Optional:    false
   QoS Class:       BestEffort
   Node-Selectors:  <none>
   Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                    node.kubernetes.io/unreachable:NoExecute for 300s
   Events:
     Type    Reason     Age   From                                                 Message
     ----    ------     ----  ----                                                 -------
     Normal  Scheduled  39m   default-scheduler                                    Successfully assigned cass-operator/cass-operator-65cf9cf944-vg9bb to gke-cluster-dse-default-pool-d339feaf-m54n
     Normal  Pulling    39m   kubelet, gke-cluster-dse-default-pool-d339feaf-m54n  Pulling image "datastax/cass-operator:1.0.0"
     Normal  Pulled     39m   kubelet, gke-cluster-dse-default-pool-d339feaf-m54n  Successfully pulled image "datastax/cass-operator:1.0.0"
     Normal  Created    39m   kubelet, gke-cluster-dse-default-pool-d339feaf-m54n  Created container cass-operator
     Normal  Started    39m   kubelet, gke-cluster-dse-default-pool-d339feaf-m54n  Started container cass-operator


