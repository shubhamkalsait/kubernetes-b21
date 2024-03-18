
# KUBERNETES

   Kubernetes is a cutting-edge technology that is constantly developing and lacks a stable version. It is said that those desiring a long-term career in DevOps should be familiar with Kubernetes as it's the future of DevOps.
   In this documentation we will learn about the orchestration tool Kubernetes. We'll talk about some of the most often requested interview questions and use cases too.




## Documentation

Although there are many distinct sources of  Kubernetes documentation are globally available, but we should always rely to the content supplied by kubernetes.io.

---[Click here for Documentation of Kubernetes.](https://kubernetes.io/docs/home/)---

## FAQ

#### Que 1] What is Kubernetes?

Answer-->
> * Kubernetes, sometimes referred to as k8s, is an open-source system or technology that automates containerised application deployment, scaling, and management.

> * It is used to easily manage several containers since it can handle grouping of containers at a single time.
       
> * It is an orchestration tool as it enables you to create application services that span multiple containers, schedule containers throughout a cluster, scale those containers, and monitor their health over time
#### Que 2] Why we use kubernetes?

Answer-->
>* Using containers to bundle and run your application is a fantastic idea. Managing the containers that execute the application and making sure there is no downtime are necessary in a production environment.

>* Another container must start in case the first one fails. That's where K8s comes to rescue.

####   Features that kubernetes provides are as follows :-
>* Load Balancing
>* Automated Rollouts and Rollbacks
>* Self Healing
>* Horizontal scaling , etc.
That's why k8s plays an crucial role in depolyment.

#### Que 3] What is Architecture of Kubernetes?

Answer-->
>* A cluster consisting of a number of nodes is created when Kubernetes is deployed:-
1. Control plane or master node
2. Worker Node




![Kubernetes-architecture](https://github.com/sd-devops12/Docker/assets/155714370/684bb83a-cb81-42f7-ab09-8819df073ae3)


##  Componants of Control plane.
#### 1] API Server.
--> It provides interface to communicate with all the nodes in cluster.

#### 2] Scheduler.
--> It decides where the new POD should be created. Assign node to newly created POD.

#### 3] Controller-Manager.
--> It is responsible for managing the state of the cluster. It manages to keep actual state and desired state same/equal.

#### 4] ETCD.
--> All the data of cluster is stored in ETCD in Key-Value pair.

##  Componants of Worker Node.
#### 1] Kubelet.
--> It acts like a agent, who makes sure that containers are running in PODS.

#### 2] Kube-Proxy.
--> It maintains the networking rules for communication with PODS.

#### 3] Docker or Container Engine.
--> A fundamental componant that empowers kube to run containers effectively.

#### 4] POD.
--> POD is a smallest entity of in the architecture which is managed by kebernetes. It is wrapper around a container and it consist one or more containers.

#### Que 4] Lifecycle of a Pod?
Answer-->
## POD Lifecycle
 ![pods-lifecycle](https://github.com/sd-devops12/Docker/assets/155714370/826d652e-3430-43f5-a0f0-056d96432213)
 
>* Step 1] The Pod spec is submitted to the API server by kubectl or any other API client.
>* Step 2] The Pod object is written to the etcd data store by the API server. An acknowledgment is returned to the client and API server after a successful write.
>* Step 3] The API server now reflects the change in the state of etcd.
>* Step 4] The Kube-scheduler observes that a new Pod object has been generated on the API server in this instance, but it is not attached to any nodes.
>* Step 5] A node is assigned to the pod via kube-scheduler, which also updates the API server.
>* Step 6] The etcd data store then receives this modification. This node assignment is also reflected in the Pod object of the API server.
>* Step 7] Every node of Kubelet additionally has watchers running on it that monitor the API server. The target node's Kubelet observes that it has a new Pod assigned to it.
>* Step 8] By contacting Docker, Kubelet launches the pod on its node and returns the updated container status to the API server.
>* Step 9] Next, the pod state is persisting into etcd by the API server.

This is the whole and sole lifecycle of a POD.