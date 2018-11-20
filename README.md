

# Kubernetes or K8s

Kubernetes (commonly stylized as K8s) is an open-source container-orchestration system for automating deployment, scaling and management of
containerized applications. It was originally designed by Google and is now maintained by the Cloud Native Computing Foundation.
It aims to provide a "platform for automating deployment, scaling, and operations of application containers across clusters of hosts".
It works with a range of container tools, including Docker, since its first release

Kubernetes defines a set of building blocks ("primitives"), which collectively provide mechanisms that deploy, maintain,
and scale applications. Kubernetes is loosely coupled and extensible to meet different workloads.
This extensibility is provided in large part by the Kubernetes API, which is used by internal components as well as extensions and containers that run on Kubernetes


# Pods

The basic scheduling unit in Kubernetes is a pod. It adds a higher level of abstraction by grouping containerized components. A pod consists of one or more containers that are guaranteed to be co-located on the host machine and can share resources.
Each pod in Kubernetes is assigned a unique IP address within the cluster, which allows applications to use ports without the risk of conflict.
A pod can define a volume, such as a local disk directory or a network disk, and expose it to the containers in the pod.
Pods can be managed manually through the Kubernetes API, or their management can be delegated to a controller


# Controllers

A controller is a reconciliation loop that drives actual cluster state toward the desired cluster state.
It does this by managing a set of pods. One kind of controller is a replication controller, which handles replication and scaling by running a specified number of copies of a pod across the cluster.
It also handles creating replacement pods if the underlying node fails. Other controllers that are part of the core Kubernetes system include
a "DaemonSet Controller" for running exactly one pod on every machine(Node) (or some subset of machines), and a "Job Controller" for running pods that run to
completion, e.g. as part of a batch job. The set of pods that a controller manages is determined by label selectors that are part of the controller’s definition.

# Services

A Kubernetes service is a set of pods that work together, such as one tier of a multi-tier application. The set of pods that constitute a service are defined by a label selector.
Kubernetes provides service discovery and request routing by assigning a stable IP address and DNS name to the service, and load balances traffic in a round-robin manner to network connections
of that IP address among the pods matching the selector (even as failures cause the pods to move from machine to machine). By default a service is exposed inside a cluster (e.g. back end pods might be grouped into a service,
with requests from the front-end pods load-balanced among them), but a service can also be exposed outside a cluster (e.g. for clients to reach frontend pods).

# Architecture

Kubernetes follows the master-slave architecture. The components of Kubernetes can be divided into those that manage an individual node and those that are
part of the control plane.

# Kubernetes control plane (master)
The Kubernetes Master is the main controlling unit of the cluster, managing its workload and directing communication across the system.
The Kubernetes control plane consists of various components, each its own process, that can run both on a single master node or on multiple masters supporting high-availability clusters.
The various components of Kubernetes control plane are as follows:

# etcd

etcd is a persistent, lightweight, distributed, key-value data store developed by CoreOS that reliably stores the configuration data of the cluster,
representing the overall state of the cluster at any given point of time. Other components watch for changes to this store to bring themselves into the
desired state.

# API server

The API server is a key component and serves the Kubernetes API using JSON over HTTP, which provides both the internal and external interface to Kubernetes.
The API server processes and validates REST requests and updates state of the API objects in etcd, thereby allowing clients to configure workloads
and containers across Worker nodes.[24]

# Scheduler
The scheduler is the pluggable component that selects which node an unscheduled pod (the basic entity managed by the scheduler) runs on, based on resource availability. Scheduler tracks resource use on each node to ensure that workload is not scheduled in excess of available resources.
For this purpose, the scheduler must know the resource requirements, resource availability, and other user-provided constraints and policy directives such as quality-of-service, affinity/anti-affinity requirements, data locality, and so on.
In essence, the scheduler’s role is to match resource "supply" to workload "demand".

# Controller manager
The controller manager is a process that runs core Kubernetes controllers like DaemonSet Controller and Replication Controller. The controllers communicate with the API server to create,
update, and delete the resources they manage (pods, service endpoints, etc.).

# Kubernetes worker node (slave)
The Node, also known as Worker or Minion, is a machine where containers (workloads) are deployed. Every node in the cluster must run a container runtime such as Docker,
as well as the below-mentioned components, for communication with master for network configuration of these containers.

# Kubelet
Kubelet is responsible for the running state of each node, ensuring that all containers on the node are healthy.
It takes care of starting, stopping, and maintaining application containers organized into pods as directed by the control plane.

Kubelet monitors the state of a pod, and if not in the desired state, the pod re-deploys to the same node. Node status is relayed every few seconds via heartbeat messages to the master.
Once the master detects a node failure, the Replication Controller observes this state change and launches pods on other healthy nodes.[citation needed]

# Container

A container resides inside a pod. The container is the lowest level of a micro-service that holds the running application, libraries, and their dependencies.
 Containers can be exposed to the world through an external IP address. Kubernetes support Docker container since its first version, in July 2016 rkt container engine was added.

# Kube-proxy

The Kube-proxy is an implementation of a network proxy and a load balancer, and it supports the service abstraction along with other networking operation.
It is responsible for routing traffic to the appropriate container based on IP and port number of the incoming request.

# cAdvisor

cAdvisor is an agent that monitors and gathers resource usage and performance metrics such as CPU, memory, file and network usage of containers on each node.

