# Kubernetes

What is kubernetes?
ubernetes is a platform-agnostic system for automating the deployment, scaling, and management of containerized applications. It helps you deploy and manage applications in a consistent and reliable manner, regardless of where they are running, and provides a way to achieve high availability by automatically replicating and rescheduling applications across multiple machine.
Kubernetes (also known as K8s) is an open-source system. It was originally developed by Google and they donated to CNCF in 2014 and is now maintained by the Cloud Native Computing Foundation (CNCF).
So, basically Kubernetes is a container orchestration tool.

Why we should use Kubernetes?
Kubernetes is its ability to automate the deployment, scaling, and management of applications in a consistent and reliable manner. It provides features such as self-healing, rolling updates, and resource management, which make it easier to deploy and manage applications at scale.

Introduction to container orchestration:-
We know that we can pack this application as the images with all its libraries and dependencies and run them as containers. So running a few containers is fine, but when you see a production-ready scenario where you want to run thousands of containers, you need container orchestration because you cannot create, manage, and do many things manually.

Kubernetes architecture:-

What is Kubelet in Kubernetes?
Firstly, the request is authenticated with the headers that are passed, and then based on the RBAC rules, it is authorized whether that particular user is allowed to create a pod. Now, the scheduler will find the best fit node for the specific pod. The scheduler has all the information about the nodes, about the resources. So based on the resources, the taints, tolerations, and node affinity, it will try to find the best fit node within the cluster to run the pod. Now, it gives the node information back to the API server. Again, it tells me that this node has to run this particular workload. Now what happens is, on the worker node side, the main component is kubelet. Also, kubelet will keep asking the API server whether I have some workload to run. As soon as the scheduler says, "Okay, this workload has to run on node one, " the API server will inform "you need to run this workload." When the kubelet gets this information, it does all the fetching of images using the container runtime. So container runtime, like Containerd or Docker, will pull the image then run the pod with the right set of defined configurations. Then a pod will run with a single or multiple containers, whatever is defined in the pod specification.

What is Kube-proxy?
Another component in worker nodes is Kube-proxy, the core network component of Kubernetes that manages all the networking and communication across the cluster. So your port-to-port communications, all the communication, all the rules are taken care of by Kube-proxy. And there is a controller manager component in the master node, which runs on the control plane. The controller manager is a set of controllers running a replication set controller. So if we create a deployment, then we define the number of replicas that we have to run, which is taken care of by the replication controller. If we make a DaemonSet object that needs this particular workload to run on all the nodes, the DaemonSet controller does that. So like this, there are different sets of controllers, and collectively it is called controller manager. It controls the Kubernetes cluster and the state within which they are running three replicas and all those things.

What is ETCD?
ETCD is a highly available key-value database for Kubernetes that stores all the information of all the resources and objects running in the cluster. Now, the API server is responsible for storing all that information in ETCD. So if any pod spec or anything there is changing, the cluster state stored in ETCD is maintained in ETCD. So the Kubernetes architecture is on a very high level. On the master node, you have an API server, which we can consider as the brain. Then, you have the scheduler that schedules the node and the controller manager having various sets of controllers that control the workloads across the cluster. Then the kubelet always communicates with the API server and keeps updating the workload status that it is running. It is also responsible for pulling the image using the container runtime and then running the pod, which is eventually the module container. Then the Kube-proxy is the networking component that makes the network communication within the cluster. And the nodes are the VMs or the bare metal machines.

![Screenshot (72)](https://user-images.githubusercontent.com/108757431/210139921-36746754-91d6-4b71-adbf-b707350d25a2.png)



Monolithic and microservice:-
monolithic and microservices. To understand the concept correctly, think of a movie ticket booking application. Now, whenever you try to book a ticket, go to the UI, sign up, book a ticket, go to the payment checkout, and get a movie ticket confirmation.

Deployment with Monolithic vs Microservice architecture:-
Monolithic applications take more time to deploy and are not a fail-fast model. In contrast, in microservices, you can deploy individual components. You can deploy daily, even hourly, when you have minimal changes. You can deploy those changes on individual components in a light production environment. So, yes, there are companies that are doing that. Whether you have a simple application or a simple component change that you want to deploy on a live application, you can do that. In contrast, in monolithic, a small change, you have to deploy the entire stack again, making a deployment a bit harder than in microservices architecture.
