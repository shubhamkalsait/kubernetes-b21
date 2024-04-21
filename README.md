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

# Kubernetes commands use cases

## 1. Common Commands 
 - 
kubectl get pod -o wide - List of nodes and pods
	
kubectl get all –all-namespaces - List all of them.

kubectl get service –all-namespaces - Get every service

kubectl get nodes –show-labels - Show labeled nodes
	
kubectl run my-nginx –image=nginx –port=80 –expose - Run nginx deployment and expose it 

kubectl run my-nginx –restart=Never –image=nginx –port=80 –expose - Run and expose the Nginx pod

kubectl run my-nginx –image=nginx –replicas=5 –port=80 - Run a two-replica nginx deployment

kubectl create –dry-run –validate -f pod-GFG.yaml - Using a dry run, verify the yaml file
