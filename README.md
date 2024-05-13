# KUBERNETES

# What is Kubernetes ?
Kubernetes is an open-source container management tool. It manages docker containers in the form of cluster.

It automates container deployment, container scaling, load balancing, also called as a container orchestration tool.

It is written in golang language.

It works brilliantly with all cloud vendors, i.e, public, hybrid & on-premises.

It was developed by Google lab in 2014.

# Why we use Kubernetes ?
There are several reasons to learn kubernetes like it can easily scale applications, self-healing, portability & automation.
It is very helpful for running microservices & distributed systems.

For example -

You have an application to deploy so, you have package it into a container & run it on a server containing a docker engine or any other container engine. Your application is created using dockerfile & host it on a port for the external world to access it.

But your whole application is only running on a single server & the request of users are increasing. 

If at that point any failure occurs it becomes an application failure. Than no one can access your application. So, to handle the single point of failure google introduced Kubernetes to scale applications.

# Why we needed Kubernetes ?
Docker does not support any feature for scaling up & down the application i.e. auto scaling.

Docker does not provide load balancing feature.

There is no any docker level authentication.

There is not any security mechanism.

There is no auto start to the container.

We cannot do routing, if you need than you will need to do it manually.

To overcome these drawbacks of docker we have docker swarm, docker compose, Kubernetes.

Kubernetes provides all this features in one place. 
It also provides basic routing & DNS facility.

# Benefits of Kubernetes -
Automated deployment & management.

Scalability.

High availability.

Cost effectiveness.

Improved developer productivity.

# Use cases of Kubernetes in real-world scenarios -
**E-Commerce -**
You deploy & manage the e-commerce websites by autoscaling & load balancing you can manage the millions of users & transactions.

**Media & Entertainment -**
You can store the static & dynamic data that can deliver it across the world without any latency to the end users.

**Financial services -**
Kubernetes is well suited for the sinical application because of the level of security it is offering.

**Healthcare -**
You can store the data of patient & take care the outcomes of the health of patient.

# Architecture of Kubernetes –
![image](https://github.com/Rinki-shrivastava/kubernetes/assets/153551978/7e4d95ca-90c1-4236-80f3-7f4467b8a0b4)

**Kubernetes – Cluster Architecture**
As can be seen in the diagram above, Kubernetes has a client-server architecture and has master and worker nodes, with the master being installed on a single Linux system and the nodes on many Linux workstations. 

**1. CLUSTER -**

A Kubernetes cluster is essentially a group of machines working together to run containerzed applications. These machine is called as nodes, can be physical servers or virtual machines. It consists of master node & multiple worker nodes.

**2. NODES -**

These are the individual machines in the cluster that run the containerized applications. There are two main types of nodes.

**Master node -**
This node controls the entire cluster, scheduling tasks & making sure everything runs smoothly.

**Worker node -**
These nodes actually run the containerized applications.

**3. Control Plane -**

It is basically a collection of various components that helps us in managing the overall health of a cluster. Basically 4 services run on control plane i.e. API server, ETCD, Scheduler, Controller Manager.

**4. API-server -**

It is like an initial gateway to the cluster that listens to updates or queries via CLI like kubectl. Kubectl communicates with API server to inform what needs to be done like creating pods or deleting pods etc. It also works as a gatekeeper. It generally validates requests received & then forwards them to other processes. No request can be directlu passed to the cluster, it has to be passed through the API server.

**5. Scheduler -**

When API server receives a request for scheduling pods that the request is passed on the scheduler. It intelligently decides on which node to schedule the pod for better efficiency of the cluster.

**6. Controller Manager -**

It is responsible for running the controllers that handle the various aspects of the cluster's control loop. It include the replication controller, which ensures that the desired no. of replicas of a given application is running & the node controller which ensures that nodes are correctly marked as ready or not ready based on their current state. It is used to match actual state & desired state.

**7. ETCD -**

It is a key-value store of a cluster. The cluster state changes get stored in the etcd. It acts as the cluster brain because it tells the Scheduler & other processes about which resources are available & about cluster state changes.

**8. Kubelet -**

Scheduler tells the Kubelet to create pod & kubelet works on it. It runs the docker commands. Kubelet interacts with both the container runtime as well as the node. It is the process responsible for starting a pod with a container inside.

**9. Kube-Proxy -**

It is used for networking in the cluster. It is the process responsible for forwarding the request from services to the pods. It has intelligent logic to forward the request to the right pod in the worker node. It enables communication between different pods & external traffic to the cluster.

**10. Container Engine -**

It is a daemon service which creates containers. This allows Kubernetes to support multiple container runtimes without direclty depending on their implementation details.

**11. PODS -**

Kubernetes manages PODS. Container run inside the PODS. PODS are the wraper around the containers. Kubernetes organizes containers into logical units called pods. Each pod can contain one or more containers that share networking & storage resources. The container engine is responsible for launching & managing these containers within the pods.

# Kubernetes Advantages

**Automatic container schedule:** Kubernetes may reschedule a container from one node to another to increase resource utilization. This means you get more work out of the same number of machines, which saves money.

**Service discovery:** When you have a bunch of services that need to communicate with each other it’s critical that they are able to find each other first. This is especially true because containers are automatically scheduled and may potentially get moved around. Thankfully, Kubernetes makes it easy for containers to communicate with each other.

**Self-Healing:** Kubernetes automatically monitors containers and reschedules them if they crash or are terminated when they shouldn’t. Kubernetes will also reschedule containers in the event that the node that they’re living on fails.

**Rolling Upgrades:** Fortunately, Kubernetes has the ability to perform rolling updates. This is where old containers are judiciously swapped out of a new version of the same containers all without disrupting the service provided by the running application.

# Lifecycle of POD -

![image](https://github.com/Rinki-shrivastava/kubernetes/assets/153551978/11ab7b40-4dd3-43d8-905f-803947d18539)

1. Users submit Pod objects to the API server through kubectl or other API clients.

2. The API server attempts to store the relevant information of the Pod object into etcd. After the writing operation is completed, the API server will return confirmation information to the client.

3. The API server begins to reflect state changes in etcd.

4. All Kubernetes components use the watch mechanism to track and check related changes on the API server.

5. kube-scheduler observed through its watcher that the API server created a new Pod object but was not yet bound to any node.

6. kube-scheduler selects a worker node for the Pod object and updates the result to the API server.

7. The scheduling results are updated from the API server to etcd, and the API server also begins to reflect the scheduling results of this Pod object.

8. The kubelet on the target worker node where the Pod is scheduled attempts to start the container on the current node and returns the resulting status of the container to the API server.

9. The API server stores Pod status information into etcd.

10. After etcd confirms that the write operation is completed, the API server sends the confirmation information to the relevant kubelet.

# Stages of a POD -

Through its lifecycle, a Pod can attain following states -

**Running -** The pod is scheduled on a node & all its containers are created & atleast one container is in Running state.

**Pending -** The pod is accepted by the Kubernetes system but its containers is/are not created yet.

**Succeeded -** All containers in the Pod have exited with status 0 & will not be restarted.

**Failed -** All containers of the pod have exited & at least one container has returned a non-zero status.

**CrashloopBackoff -** The container fails to start & is tried again & again.

# What is EKS ?
Amazon EKS is a managed service that eliminates the need to install, operate & maintain your own Kubernetes control plane on AWS. Kubernetes is an open-source system that automates the management, scaling, & deployment of containerized applications.

# Features of EKS -
1. Secure networking & authentication.
2. Easy cluster scaling.
3. Managed Kubernetes experience.
4. High availability.
5. Integration with AWS services.
6. Advanced workload Support.
7. Open-source compatibility.

# Kubernetes Objects -

**1. Node -**
In kubernetes, a node object represents a worker machine containerized applications actually run. This machine can be a physical server or a virtual machine(VM). It serves as a communication channel between the control plane & worker machines, enabling scheduling, resource management & health monitorining.

**2. Pods -**
The fundamental unit in Kubernetes. A Pod represents a single instance of a running application, encapsulating one or more containers that share storage & network resources. Can run multiple containers in a single pod.

**3. Services -**
Act as an abstraction layer for pods, enabling them to be accessed by external applications or services. Services provide a stable network identity for Pods, even if they are recreated or rescheduled.

**4. Namespace -**
Organize & isolate resources within a cluster. Namespaces allow multiple users or projects to run kubernetes objects without conflicts.

**5. Replication Controller -**
RCs are legacy API object in kubernetes used for managing pod lifecycle & ensuring a desired no. of pod replicas are running at any given time.

**6. Replicaset -**
Guarantee a specific no. of pod replicas are running at all times. Deployments utilize Replicasets internally to manage pod creation & deletion.

**7. Deployment -**
Manage the lifecycle of Pods & ensure a desired no. of replicas are running for your application. Deployments automate deployments and rolling updates, enabling controlled application versioning.

**8. Stateful set -**
Designed for stateful applications that requires persistent storage & unique identities. Stateful sets maintain a desired no. of ordered Pods, ensuring their startup order & persistent storage.

**9. Deamon set -**
Ensure exactly one or more Pods run on all cluster nodes. DaemonSets are useful for system tasks like logging or monitoring agents that need to run on every node.

**10. Config map -**
A ConfigMap in kubernetes is used to store configuration data, such as environment variables or configuration files, separate from the application code. It allows for easy management & updated of configuration settings without modifying the application itself. It is an API object used to store non-sensitive configuration data in key-value pairs that can be consumed by pods or other kubernetes objects.

**11. Secrets -**
In kubernetes, a secrets object is a vault for storing sensitive information like passwords, API keys, or tokens used by your applications. It acts like a secure way to keep your "crown jewels" hidden from unauthorized access.

**12. HPA -**
An HPA object in kubernetes, which stands for Horizontal Pod Autoscaler, is king of like an automatic thermostat for your applications. It helps scale your application up or down based on its resource usage.

**13. Ingress -**
It acts as a gateway to your services running inside the cluster. Its like a door & doorman for external traffic trying to reach your applications. It sits at the entrance & welcomes external traffic.

**14. PV & PVC -**
Provide persistent storage for Pods. PVs (Persistent Volume)  represent the actual storage available (e.g., host directory, cloud storage), while PVCs (Persistent Volume Claims) are requests from Pods for storage resources.

**15. Jobs -**
Used to run a set of Pods to completion. Jobs are ideal for one-time tasks or batch processing jobs that don't require continuous operation.


















