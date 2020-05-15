Glossary
********

.. glossary::

  Sphinx
    Sphinx is a tool that makes it easy to create intelligent and beautiful documentation. It was originally created for the Python documentation, and it has excellent facilities for the documentation of software projects in a range of languages.
    
  Cassandra Operator
    DataStax Kubernetes Operator for Apache Cassandra® (Cassandra Operator) automates the process of deploying and managing open-source Apache Cassandra® or DataStax Enterprise (DSE) in a Kubernetes cluster.

  Namespace
    Namespaces are intended for use in environments with many users spread across multiple teams, or projects. For clusters with a few to tens of users, you should not need to create or think about namespaces at all. Start using namespaces when you need the features they provide. Ref: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/

  Service Account
    When you (a human) access the cluster (for example, using kubectl), you are authenticated by the apiserver as a particular User Account (currently this is usually admin, unless your cluster administrator has customized your cluster). Processes in containers inside pods can also contact the apiserver. When they do, they are authenticated as a particular Service Account (for example, default).

  ServiceMonitor 
    Describes the set of targets to be monitored by Prometheus

  spec
    The spec declares the desired state of a resource which includes configuration settings provided by the user, default values expanded by the system, and other properties initialized by other internal components after resource creation. 

  Management API
    The Management API is a sidecar service layer that attempts to build a well supported set of operational actions on Cassandra® nodes that can be administered centrally. It currently works with official Apache Cassandra® 3.11.x an 4.0 via a drop in java agent. For more information refer to https://github.com/datastax/management-api-for-apache-cassandra.

  
