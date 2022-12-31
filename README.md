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

![Screenshot (71)](https://user-images.githubusercontent.com/108757431/210139868-da85e399-c8e8-4e9a-a000-efe78bdc1362.png)


Monolithic and microservice:-

monolithic and microservices. To understand the concept correctly, think of a movie ticket booking application. Now, whenever you try to book a ticket, go to the UI, sign up, book a ticket, go to the payment checkout, and get a movie ticket confirmation.

Deployment with Monolithic vs Microservice architecture

Monolithic applications take more time to deploy and are not a fail-fast model. In contrast, in microservices, you can deploy individual components. You can deploy daily, even hourly, when you have minimal changes. You can deploy those changes on individual components in a light production environment. So, yes, there are companies that are doing that. Whether you have a simple application or a simple component change that you want to deploy on a live application, you can do that. In contrast, in monolithic, a small change, you have to deploy the entire stack again, making a deployment a bit harder than in microservices architecture.
