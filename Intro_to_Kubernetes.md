# Learn Kubernetes Basics

Guide to [Kubernetes](https://kubernetes.io/docs/tutorials/kubernetes-basics/)

## Kubernetes Clusters

Kubernetes coordinates a highly available cluster of computers that are connected to work as a single unit. Applications runs on containers, and containers are manipulated by Kubernetes, which automate the distribution and scheduling of application containers across a cluster in an efficient way. 

A **Kubernetes cluster** has two types of resources:
 - **Control Plane**: 
   - Coordinates the cluster
 - Nodes: 
   - Actual workers that run the applications in node processes.
   - A Kubernetes cluster has at least three nodes to ensure redundancy
   - Each node is a VM or a physical computer that serves as a worker machine in a Kubernetes cluster.
   - Every Kubernetes Node runs at least:
        - **Kubelet**, a process responsible for communication between the Kubernetes control plane and the Node; it manages the Pods and the containers running on a machine.
        - A container runtime (like Docker) responsible for pulling the container image from a registry, unpacking the container, and running the application.

**Note:** All Kubernetes are defined using YAML (preferred) or JSON files.
  
When applications are deployed, the user tells the control plane to start the application containers. The control plane then schedules the containers to run on the cluster nodes. Nodes communicate back to the control plane through the **Kubernetes API** that the control plane exposes.

**Aside:** Minikube is a lightweight Kubernetes implementation that creates a VM on the local machine and deploys a simple cluster containing of only one node.

## Deployment

Once a Kubernetes cluster is created, applications which are to be deployed are specified in the Kubernetes **Deployment configuration**. This configuration tells Kubernetes how to create as well as *update* instances of the application. 

Once application instances are deployed, a Kubernetes **Deployment Controller** continuously monitors the instances. If an instance goes down, the Deployment Controller automatically schedule a new instance to be run (allowing a **self-healing mechanism** to deal with machine failure or maintenance). This functionality marks a step from previous deployment strategies, in which only an installation script is provided but no recovery process is established at the start.

Scaling is accomplished by changing the number of replicas in a Deployment

### Kubectl

Kubernetes offers **Kubectl**, which is the command line interface that uses the Kubernetes API to interact with the cluster. Common commands include:

- kubectl get - list resources
- kubectl describe - show detailed information about a resource
- kubectl logs - print the logs from a container in a pod
- kubectl exec - execute a command on a container in a pod


## Pods

When a Deployment configuration is created, Kubernetes also create a **Pod** to host the application instance. A Pod is an abstraction that represents of a group of one or more application containers and some shared resources for those containers (which can include shared storage, network, information how to run each container, etc.). The Pod is often used to contain different application containers which are relatively tightly coupled.

Pods are the **atomic unit** on the Kubernetes platform. Each Pod is tied to the Node where it is scheduled, and remains there until termination or deletion. A Node can have multiple pods.

Pods have a lifecycle, which expires when a worker node dies. A **ReplicaSet** might then dynamically drive the cluster back to a desired state via creation of new Pods to keep the application running. For example, a cluster may be running with multiple replicas of the same pod (this is an abstracted away in the front end). The ReplicaSet is responsible for reconciling changes among Pods so that the application continues to function and dealing with failures.

Also it's important to not that each Pod in a Kubernetes cluster has a unique IP address (even among Pods in the same Node). Although each Pod has a unique IP address, those IPs are not exposed outside the cluster without a **Service**.

## Service

A **Service** in Kubernetes which defines a logical set of Pods and a policy by which to access them. Services are the abstraction that  pods to die and replicate in Kubernetes without impacting the application. Services allows loose coupling between dependent pods (interconnection at even a higher level than just images *within* a Pod). The set of Pods targeted by a Service is usually a *LabelSelector*. 

A Service routes traffic across a set of Pods. Discovering and routing among dependent Pods (such as frontend and backend of an application) is handled by Kubernetes Services.

Services match a set of Pods using labels and selectors, a grouping primitive that allows logical operation on objects in Kubernetes. Labels are key/value pairs attached to objects and can be used in any number of ways:
 - Designate objects for development, test, and production
 - Embed version tags
 - Classify an object using tags
