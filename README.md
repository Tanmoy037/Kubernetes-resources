# Kubernetes

**1)What is kubernetes?**

ubernetes is a platform-agnostic system for automating the deployment, scaling, and management of containerized applications. It helps you deploy and manage applications in a consistent and reliable manner, regardless of where they are running, and provides a way to achieve high availability by automatically replicating and rescheduling applications across multiple machine.
Kubernetes (also known as K8s) is an open-source system. It was originally developed by Google and they donated to CNCF in 2014 and is now maintained by the Cloud Native Computing Foundation (CNCF).
So, basically Kubernetes is a container orchestration tool.

**2)Why we should use Kubernetes?**

Kubernetes is its ability to automate the deployment, scaling, and management of applications in a consistent and reliable manner. It provides features such as self-healing, rolling updates, and resource management, which make it easier to deploy and manage applications at scale.

Introduction to container orchestration:-

We know that we can pack this application as the images with all its libraries and dependencies and run them as containers. So running a few containers is fine, but when you see a production-ready scenario where you want to run thousands of containers, you need container orchestration because you cannot create, manage, and do many things manually.

**3)Kubernetes architecture :-**

What is Kubelet in Kubernetes?

Firstly, the request is authenticated with the headers that are passed, and then based on the RBAC rules, it is authorized whether that particular user is allowed to create a pod. Now, the scheduler will find the best fit node for the specific pod. The scheduler has all the information about the nodes, about the resources. So based on the resources, the taints, tolerations, and node affinity, it will try to find the best fit node within the cluster to run the pod. Now, it gives the node information back to the API server. Again, it tells me that this node has to run this particular workload. Now what happens is, on the worker node side, the main component is kubelet. Also, kubelet will keep asking the API server whether I have some workload to run. As soon as the scheduler says, "Okay, this workload has to run on node one, " the API server will inform "you need to run this workload." When the kubelet gets this information, it does all the fetching of images using the container runtime. So container runtime, like Containerd or Docker, will pull the image then run the pod with the right set of defined configurations. Then a pod will run with a single or multiple containers, whatever is defined in the pod specification.

What is Kube-proxy?

Another component in worker nodes is Kube-proxy, the core network component of Kubernetes that manages all the networking and communication across the cluster. So your port-to-port communications, all the communication, all the rules are taken care of by Kube-proxy. And there is a controller manager component in the master node, which runs on the control plane. The controller manager is a set of controllers running a replication set controller. So if we create a deployment, then we define the number of replicas that we have to run, which is taken care of by the replication controller. If we make a DaemonSet object that needs this particular workload to run on all the nodes, the DaemonSet controller does that. So like this, there are different sets of controllers, and collectively it is called controller manager. It controls the Kubernetes cluster and the state within which they are running three replicas and all those things.

What is ETCD?

ETCD is a highly available key-value database for Kubernetes that stores all the information of all the resources and objects running in the cluster. Now, the API server is responsible for storing all that information in ETCD. So if any pod spec or anything there is changing, the cluster state stored in ETCD is maintained in ETCD. So the Kubernetes architecture is on a very high level. On the master node, you have an API server, which we can consider as the brain. Then, you have the scheduler that schedules the node and the controller manager having various sets of controllers that control the workloads across the cluster. Then the kubelet always communicates with the API server and keeps updating the workload status that it is running. It is also responsible for pulling the image using the container runtime and then running the pod, which is eventually the module container. Then the Kube-proxy is the networking component that makes the network communication within the cluster. And the nodes are the VMs or the bare metal machines.

![Screenshot (72)](https://user-images.githubusercontent.com/108757431/210139921-36746754-91d6-4b71-adbf-b707350d25a2.png)



4)Monolithic and microservice:-

monolithic and microservices. To understand the concept correctly, think of a movie ticket booking application. Now, whenever you try to book a ticket, go to the UI, sign up, book a ticket, go to the payment checkout, and get a movie ticket confirmation.

Deployment with Monolithic vs Microservice architecture:-

Monolithic applications take more time to deploy and are not a fail-fast model. In contrast, in microservices, you can deploy individual components. You can deploy daily, even hourly, when you have minimal changes. You can deploy those changes on individual components in a light production environment. So, yes, there are companies that are doing that. Whether you have a simple application or a simple component change that you want to deploy on a live application, you can do that. In contrast, in monolithic, a small change, you have to deploy the entire stack again, making a deployment a bit harder than in microservices architecture.

5)Kubernetes object:-

In Kubernetes, everything happens by the Kubernetes objects. So whatever we want to create, we are creating a Kubernetes object. Now to start, there are two ways. One is the imperative way, and another way is the declarative way via the YAML files. You can also use JSON to create the objects directly or the curl commands, or the CLI SDKs if you are into programming or want to make the resources via the codes.

6)View API resources command:-

Also, if you want to see the API resources, use the command kubectl api-resources. You will see all the API resources that we can create and some of the short names that we can use. For namespaces, you can use the command kubectl get namespace or kubectl get ns. So you can see the short names. All the API versions of different objects have a listing on the resource list. If you're unsure which object belongs to which API version, you can see them from using kubectl api-resources.

6)Kubernetes namespace:-

In Kubernetes, namespaces are a way to provide isolated environments to different teams or groups within the same cluster with the specific amount of resource quota and other policies enforced. You can think of it as multiple virtual clusters within the same physical cluster or the same cluster.

7)Deployment:-

 Let's start by creating a deployment using the kubectl create deployment demo --image=nginx --replicas=3 --port=80 command. Our deployment is created, and we can verify it through kubectl get deploy. We can see it's rolling out, and we can check the status using the kubectl rollout status deployment demo command. We can see that it has successfully rolled out; as a result, we should have three pods running. With the kubectl get pods command, we can see the three pods with the nginx image running.

Setting an image in a deployment
By default, internally, the replica set automatically gets created with the deployment. We will verify it through the kubectl get rs command. We can see a replica set with a randomly generated hash, and you can see the same hash here with an additional string attached to it. You can see the replica set that has been created. We've specified the desired and current state and how many of them are ready. So, as of now, all pods are in a ready state.

Now, suppose we want to change the image that is running. We will use the kubectl set image deployment/demo --nginx=nginx:1.15.0 --record command. You will see that our image has been updated. Now with the kubectl rollout status deployment demo command, we can see that it's rolling out. It is finishing rolling out, which is how the rolling update works. Hence, it's a 0 downtime upgrade where you have one new pod created, then the traffic routes to that, and the previous one gets deleted once the new pod is ready.

We can see it in more detail. We will apply the kubectl get rs command, and you can see that we have a new replica set, which is 54b, whatever the complete number is. The previous one goes to 0, and the new one goes to 3.

Now, if we use the kubectl get deploy command and we describe the deployment through kubectl describe deployment demo, we'll be able to see what has happened with this in the event section. Let's see that. We can see that 54b is the newer one, and we can also see that initially, it was three deployments. When we changed the image, 54b scaled up to 1. Now, the previous one went down to 2. And then the newer one, 54b, scaled up to 2. This is how the rolling update is working. You can also see the strategy over here. It's a rolling update strategy where you have 25% max unavailable and 25% max surge, which you can also define in the deployment YAML file. This means that 25% of the pods can be unavailable at max during the update, and 25% of the pods can be maximum, meaning they can be an additional pod that can be spurned up. So to what extent, how many pods should there be? It can expect 25% extra of the existing desired state at the time of the update. We have seen the replica set, and also we can see the pods. One more thing we can see is that we changed the image. So now the image of the container is nginx 1.15.0.

What happens when a wrong image is set in a deployment?
Sometimes, what happens is that supposedly we have given the wrong image. Let's give a wrong image. Hence we'll go back, giving the following command: kubectl set image deployment/demo --nginx=nginx:1.15.abc --record. You will see that it gets updated, but it'll not completely update because we have given the wrong image. If we use the kubectl get pods command, we can see that the pods are running, but it created an extra pod. So the max surge came into the picture, creating an extra pod, and the image ErrPull came. Hence, this pod never got ready, and that's why the previous one never got terminated. That's how it takes care, and the deployment will take care. Now, if we want, we can use the kubectl get rs command as well. There should be three now; this one is the newer one, which isn't ready.

Rollbacking from a wrong image deployment
We can also do a rollback. Now, how can we do a rollback? By undoing the deployment, basically. We can first see the status through the kubectl rollout history deployment demo command. Now, let's use the rollout command kubectl rollout undo deployment demo --to-revision=2, and we have rolled back. Next, we can use the kubectl get rs command, and we can see that this one will be used as a test, and now, if we use the kubectl get pods command, we can see that we have rolled back. That's how rollback happens. Sometimes the deployment can go wrong. There can be some issues. So that's why this particular feature also helps.

Scaling a deployment
Another thing that can be done is we can scale the deployment. For that, use the kubectl scale deployment demo --replicas=5. We can see that it has been scaled. Now, if we see, we should have five pods, two of which are in ContainerCreating, which is perfectly fine. So we have five pods, and our desired state has been changed to 5, and if we use the kubectl get rs command, we can see it has been changed to 5.

8)What are StatefulSets?

StatefulSet is a Kubernetes object which is used for Stateful applications such as databases. However, there are cases just like databases where you need persistence, or you need to store the state of the application, which Deployments cannot serve.

9)What is a Headless service and why is it important for StatefulSets?

Another important thing to note over here is that we have to use headless services for Stateful applications. A headless service is a service where the cluster IP is none. But why a headless service? Because if we talk about any services, it can serve traffic to any of the instances. But we cannot afford that when we are using a database application. You can see that this is the web-0 pod, and this is web-1 which is maybe a MySQL database. When you have a service over here, it automatically sends the right operation to this and the next one. It sends the right operation to this, leading to data inconsistency. Here we need to maintain a master/slave architecture with the configuration we have to define, but we know the order. We can predefine that web-0 will be the master and web-1 will be the slave because we know the order, and there can be data replication. As a result, whenever a new pod comes up, it replicates the data and will be in the same state as the previous pod. So there has to be a replication mechanism that we have to handle.

But what Kubernetes can do is, if you have a headless service over here, we remove this particular service, and we type our headless service over here. Now, when you have a headless service, what will happen is that each pod will get its unique network identity as well, which can be referred to when you are doing the replication because you will know what the headless service name is. Also, when we create the specification for StatefulSet, we will define the service name.

We will define the service name, and we'll be creating the service. Now, Kubernetes helps you manage the StatefulSet, which will help you keep the sticky state session for the pods. However, there are certain aspects that a user must maintain, such as the creation of the headless service. Now, if the data is persistent, it will use PVC or a Persistent Volume Claim. Now, for that, the persistent volume or the volume provisioner has to be taken care of by the user, or they have to be pre-created by the user. It is because this particular thing will be two whenever a new pod comes in place or whenever we scale. Again, whatever the replication method we have created, it will replicate and create a PVC, which will then get connected to or attached to a PV. Then if you have any external mechanism for the external storage, that can be used, but that has to be set by the user.

The scaling will also get a unique identifier and a unique network identifier because it is a StatefulSet. Hence, whenever the deletion happens, deletion also happens in the previous reverse order. So, the last created pod will be the first one to go with the scale down, and then the others will follow, and this is how the scaling down also happens in the reverse order. The scaling up happens in this way where you know what will be the next pod name and the following network identity of the pod name.

8)What are DaemonSets?

DaemonSets in Kubernetes ensure that a copy of the pod runs on all or some nodes. Whenever a new node joins, the same copy of the pod is pinned over there, and whenever a node is removed from the cluster, the pod also gets removed. The DaemonSet controller controls DaemonSet, which is scheduled on all the pods, except for the ones where you cannot schedule the pods, or it's not schedulable, like on a master node.


9)How does container-to-container networking take place?

Firstly, we have an ethernet device that allows for network traffic in and out of the virtual machine. But on top of this, we have a network namespace. Network namespace is the ability to partition the network layer into isolated stacks per process. Hence, we have a root network namespace, but what we're going to do is when we create a new pod, we define the pod as having its own network namespace. So, in this occurrence, we'll call it mypodns which approximately amounts to /var/run/netns/mypodns as a file directory path, and that is a mount point for the processes from our containers.

This also means the second part is that when we launch a container, we have to rely upon the docker command of the net container function to link these containers into the pod network namespace. This means the pods can communicate as if they're on the local host. In conjunction with this, the mypod network namespace is attached to the root network namespace, allowing communication with the outside world.


10)What is a Container Network Interface (CNI)?

Today we're going to talk about container network interfaces. The CNI project and CNCF help combine various network technologies and produce a set of plugins that can be switched in and out of Kubernetes clusters through the kubelets to offer different features and use cases. They are a requirement for inter-node networking, and there are many different options and flavors. Some offer VXLAN capabilities, dual stacking, extended Berkeley Packet Filter, logging, etc. But essentially, they're all designed so that you can talk between containers at the base layer. The reason that CNI is popular and why it was necessary is that Kubernetes doesn't provide its own networking implementation, it just defines the model, and it leaves us to fill the gaps and build that model out.

11)What is Flannel and how does it work?

Flannel is a CNI that is fairly simplistic but represents the power, and we can also follow through on how it creates inter-host networking. It's a virtual network layer encapsulated, and in this example, we can see we have a VPC, and this VPC could be an AWS VPC or any other cloud provider. We have a /19 at the top level of addressable IPs in this VPC. We then have something called a Flannel pod network, which is a /16. So, instantly you can see that this is a much larger address range than the VPC level of the /19, and, you know, that's 65,536 addressable IPs in there. In addition, we also then get with Flannel the ability to carve up at the host level as well as at the machine level. Then you'll get, in fact, a /24 on each of these host machines. What's important about that is that this gives you three layers of addressable IP ranges, and it also forms the backbone of how Flannel will do the subnet to host mapping, which we'll talk about later.

There's a simple flat overlay network that gets created inside of your VPC on your cluster. Essentially, we'll follow the journey of how a packet would be sent from one virtual machine or one Kubernetes node to another in the cluster and then understand how to route it to the right pod. In this example, let's pick this pod here with the container 100.96.1.2, and we want to send it to a pod on this host within the cluster over here. This host might have many other containers and pods within that are operating and running on this host. Therefore, we need a way to route the IP packets to the destination accurately. Let's think about how these will look. We have our source and destination here, but how will that journey look? The first thing that happens, as we spoke about previously, is that we cross the network namespace within the pod, go across the veth pair and down to the L3 Linux bridge, and that bridge then forwards the packets through to the flannel0. Now, flannel0 is a TUN device simulating a network layer device, and it operates by sending bidirectional packets between the userland and the kernel. This is the cornerstone of how Flannel works because it can intercept operations coming out of the kernel level space.

What effectively happens is when flannel0 is set up, flanneld will be setting up kernel routing table rules. This means packets are dropped through flannel0 when they are identified as part of the wider /16 overlay network. They go into the kernel, and the kernel lane attempts to route these packets but ultimately decides to push them back up through the TUN0 device, which is forwarded instead to the flanneld daemon process. This daemon process is where all of the logic happens. The daemon process can query etcd for the subnet range of the target host IP, and that subnet range can be resolved to the underlying VM VPC level address.

It then uses a UDP Send to the node in question, which is intercepted by the flannel daemon running there, which performs the inverse activity going down through the flannel0 tunnel into the kernel, then back up. Still, the routing table will push it towards the local Docker bridge. It will move up over the L3 into the veth, across the network namespace, and up into the container. Therefore, that illustrates how Flannel enables quite an esoteric problem in a very simplistic way. It gives us a ton of addressable IPs and enables us to plug this in and not think about it too much so that once it's configured, it just starts working. The thing to say about Flannel in terms of performance is that there is a penalty of the transaction between user and kernel level that other CNIs have ways around by slightly different implementations. And this is one of many of a variety of implementations on how to use IPAM and send IP packets across the network.

12)kubernetes services:-

In Kubernetes, a Service is an abstraction that defines a logical set of Pods and a policy by which to access them. For example, a single Service might expose a set of Pods as a backend for a load balancer. Services are used to expose the functionality of your applications to other applications and users.

There are several types of Services in Kubernetes, including:

ClusterIP: Exposes the Service on a cluster-internal IP. It is only reachable from within the cluster.
NodePort: Exposes the Service on each Node's IP at a static port (the NodePort). You can reach the Service by requesting <NodeIP>:<NodePort>.
LoadBalancer: Exposes the Service externally using a cloud provider's load balancer.
ExternalName: Maps the Service to the contents of the externalName field (e.g. foo.bar.example.com), by returning a CNAME record with its value.
You can read more about Services in the Kubernetes documentation: https://kubernetes.io/docs/concepts/services-networking/service/

13)What is ClusterIP?

 ClusterIP is the default type. So, if you don't specify any type, this will be used. In ClusterIP, our endpoint, our service, will only be accessible from within the cluster, not from the outside world. ClusterIP is not used to route traffic from the outside world, only traffic within the cluster. So, anything happening within a cluster can be routed through ClusterIP.
the service describes the different rules and configurations used to access our different pods or deployment resources. So, if we go ahead and check everything that we have within our Kubernetes by using the command kubectl get all -n example, we can see that I have redeployed the service. Now, we have ClusterIP running. We have a ClusterIP endpoint. Now, this is the endpoint, the IP address accessible within the cluster only. And then we have here the port over which it's accessible. So, now, we have the different resources that I described before.

14)NodePort:-

if we have our Kubernetes cluster and different nodes running within this cluster, they all will have different endpoints that we can connect to. So now, in the case of ClusterIP, our IP address will only be accessible from within the nodes within our cluster, they won't be accessible cluster-wide, and this is where type NodePort comes in.

We have the nodes and services. And then, we want to connect dynamically with the different nodes within the environment, and we want to have a standard way of connecting to those different nodes. And this is where we can specify NodePorts.

With NodePorts, we can specify a range of ports between 30,000 to 32,000. So, it's like the port address. And then we have, for instance, a port NodePort of 31,520 or something, something like that, specified for our NodePort. Now, it's only accessible within that range. So, in most cases, you want Kubernetes to choose the NodePort for you within the different range, and then you can configure external traffic. So, let's say there is traffic from the outside world, and we want to route the traffic into our cluster. We can then set up our load-balancing traffic routing solution, and they will all connect to our NodePort here.

15)What is a load balancer?
 
 We can use the type LoadBalancer. A LoadBalancer, basically as a type-service, allows us to dynamically route the traffic between services to those different pods within those different nodes. So, we will be able to access from the outside world through an external IP address, our application running within our Kubernetes cluster. Now, I'm telling you to be careful because this will open up an external IP address to your application without any additional rules. So, that's where in most cases, you would want to use an ingress or a service mesh of sorts that utilizes ingress to access your application from the outside world.
 
16)Now, emptyDir volume gets created as soon as the Pod is assigned to the node and it stays throughout the lifespan of the Pod. But with the deletion of a pod, the emptyDir also gets a removal. There can be specific use cases that emptyDir can be used, such as the scratch space for some sorting algorithm or the checkpointing of a long computation in the RAM.

EmptyDir can be either based on the node's disk attached to the node or, if you specify the emptyDir medium over here instead of the empty braces, it will create a temporary TMPFS and use the RAM as the volume for that. So we can write it in a yaml file, then in the container section, we can see the image, name, and command, which is simple. Now, this is the critical piece where we define the emptyDir volume. To specify, in the volume section, we say emptyDir: {} if you want the disk volume or the medium as memory or if you want to have RAM. Then next is the volumeMount, where we mount that specific emptyDir into a particular directory inside the container. So this was all about emptyDir.

17)What is a hostPath?

A hostPath volume mounts a file or a directory from the node's file system into the Pod. A hostPath will mount a directory, which is present on the node and mounted inside the container.

