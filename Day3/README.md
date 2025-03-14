# Day 3

## Info - Container Orchestration Platform Overview
<pre>
- provides an environment that gives all the features required to make our applicaiton highly available
- provides inbuilt
  - load balacing
  - monitoring
  - repair & self-healing features
  - when user-traffic increases to your application, container orchestration platform could scale up additional application instance to respond to multiple users quickly
  - when user-traffice reduces to your application, it could scale down idle application instances reducing cost
- rolling update
  - is a feature that allows upgrade your live application from one version to the other without any downtime
- rollback
  - when the newly performed rolling update if found unstable, if required it is possible to roll-back to previous stable version of your application without any down time
- service
  - is a way we can access group of load balanced application instances with a common name
  - service discovery - accessing a service by its name rather than IP address
- Examples
  - Docker SWARM
  - Kubernetes
  - Openshift
</pre>

## Info - Kubernetes Overview
<pre>
- container orchestration platform from Google
- developed in golang as an opensource project
- time tested, production grade orchestration platform
- supports CLI 
- it supports a minimal Dashboard (Web Interface)
- it supports basic building blocks
  - we can add our custom resources by defining Custom Resource Definitions (YAML with some schema)
  - In order to manage our Custom resources we need to implement Custom Controllers
  - the combination of many custom resources and customer controller is called Operator
  - using operators we can add many additional features on top of kubernetes
</pre>

## Info - Red Hat Openshift
<pre>
- it is developed on top of Kubernetes
- it is an enterprise product, that requires buying license from Red Hat
- it comes with Internal Container Registry out of the box
- it comes with Prometheus and Grafana pre-integrated to collect performance metrics and plot them into useful graphs
- it comes with user management
- it supports both CLI and Web Interface
- Web Interface very friendly, supports many powerful features that are not readily available in Kubernetes
- Adds many new features on top of Kubernetes
- Best Practices are enforced rather than just preaching(Kubernetes)
- Red Hat Openshift
  - We can only install Red Hat Enterprise CoreOS(RHCOS) in Master Nodes
  - We can install either RHEL or RHCOS in case of Worker Nodes, RHCOS is better choice though RHEL will work
  - ports upto 1024 are reserved for Red Hat Openshift, not available for user applications
  - many folders are treated read-only, if applications attempt to modify them, those applications will not run due to permission issue
  - applications should run as normal user(non-admimistrator), if they attempt things as admin, they won't be allowed to run
</pre>

## Info - Kubernetes High Level Architecture
![architecture](KubernetesArchitecture2.png)

## Info - Openshift High Level Architecture
![architecture](openshiftArchitecture.png)
![architecture](master-node.png)

## Info - Pod Overview
<pre>
- is a group of related containers
- is a logical grouping of related containers
- Pod is the smallest unit that can be deployed into Kubernetes/Openshift 
- each Pod represents one application
- every Pod has atleast 2 containers
- every Pod has secret hidden infra-container called pause container
- the pause container is not counted or revealed by Openshift 
- the pause container gets created automatically, which supports networking i.e IP address, network stack, etc.,
- in Kubernetes/Openshift, IP address is assigned only on the Pod level, not on the container level
- this is a database record/entry stored in etcd database
</pre>
![pod](PodUpdated.png)

## Info - ReplicaSet
<pre>
- replicaset is the configuration that helps us convey, how may Pod instances must be running
- it will describe desired count of pods, actual count of pods, numbers of pods that are ready
- this is maintained in etcd database as a database record/entry
</pre>

## Info - Deployment
<pre>
- deployment is a configuration that helps us deploy our application, it captures the below information
  - name of the deployment
  - container image that must be used to deploy the application
  - number of pods that are supposed to running
  - this is yaml file or database record stored in etcd database in master nodes
</pre>

## Info - Deployment Controller
<pre>
- In Master node, there is a Controller Manager component which is a collection of many controller
- Deployment Controller is one of the Controller that is part of Controller Manager
- Each Controller manages one Resource, in this case Deployment Controller manages Deployment resource
- Deployment Controller accepts Deployment as the input and it starts it work
- Deployment Controller will create the ReplicaSet configuration to create the number of Pods mentioned by the user while issuing  the deployment command
</pre>

## Info - ReplicaSet Controller
<pre>
- ReplicaSet controller takes ReplicaSet as the input and then it creates Pod as per the ReplicaSet
</pre>
