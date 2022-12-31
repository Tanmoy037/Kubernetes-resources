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

Kubernetes object:-

In Kubernetes, everything happens by the Kubernetes objects. So whatever we want to create, we are creating a Kubernetes object. Now to start, there are two ways. One is the imperative way, and another way is the declarative way via the YAML files. You can also use JSON to create the objects directly or the curl commands, or the CLI SDKs if you are into programming or want to make the resources via the codes.

View API resources command:-

Also, if you want to see the API resources, use the command kubectl api-resources. You will see all the API resources that we can create and some of the short names that we can use. For namespaces, you can use the command kubectl get namespace or kubectl get ns. So you can see the short names. All the API versions of different objects have a listing on the resource list. If you're unsure which object belongs to which API version, you can see them from using kubectl api-resources.

Kubernetes namespace:-

In Kubernetes, namespaces are a way to provide isolated environments to different teams or groups within the same cluster with the specific amount of resource quota and other policies enforced. You can think of it as multiple virtual clusters within the same physical cluster or the same cluster.

Deployment:-

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


