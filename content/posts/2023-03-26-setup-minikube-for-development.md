---
layout: post
title: How to setup minikube for development with kubernates.
author: digvijayb
tags:
  - kubernetes
  - docker
  - minikube
date: 2023-03-26T09:59:42.780Z
description: Kubernetes is an open-source container orchestration platform used for deploying, scaling, and managing containerized applications. Setting up Kubernetes on your local development system can be a great way to learn and experiment with the platform before deploying applications in a production environment. In this blog post, we will guide you through the process of setting up Kubernetes on your local development system.
thumbnail: /images/uploads/featured.png
---
Kubernetes is an open-source container orchestration platform used for deploying, scaling, and managing containerized applications. Setting up Kubernetes on your local development system can be a great way to learn and experiment with the platform before deploying applications in a production environment. In this blog post, we will guide you through the process of setting up Kubernetes on your local development system.

### Step 1: Install Docker
Before installing Kubernetes, you need to install Docker on your local system. Docker is used to build, run, and manage containers. You can download Docker for your operating system from the official Docker website.

### Step 2: Install Kubernetes
There are various ways to install Kubernetes on your local development system. In this guide, we will use Minikube, a tool that allows you to run a single-node Kubernetes cluster on your local machine.

#### To install Minikube, follow the steps below:

Install a virtualization software such as VirtualBox or Hyper-V. This is required to create a virtual machine that will host the Kubernetes cluster.

1. Download and install Minikube from the official Minikube website.

1. Open a terminal window and start Minikube by running the command below:

        `minikube start`

    This will start a virtual machine that will host the Kubernetes cluster.

1. Verify that the cluster is running by running the command below:

        `kubectl cluster-info`

This should display the endpoint and the status of the Kubernetes cluster.

### Step 3: Deploy an Application

Now that you have a running Kubernetes cluster on your local development system, you can deploy your first application to the cluster. In this example, we will deploy a simple web application using a Docker container.

1. Create a deployment by running the command below:

    `kubectl create deployment hello-world --image=gcr.io/google-samples/hello-app:1.0`

    This will create a deployment named `hello-world` with a single replica running the `hello-app` container image.

1. Expose the deployment by running the command below:

    `kubectl expose deployment hello-world --type=NodePort --port=8080`

    This will create a service that exposes the deployment to the external network.

1. Get the URL of the application by running the command below:

    `minikube service hello-world --url`

    This should display the URL of the application that you can access from your web browser.

### Step 4: Scale the Application

One of the benefits of Kubernetes is the ability to scale applications easily. In this step, we will scale the `hello-world` deployment to three replicas.

1. Scale the deployment by running the command below:

    `kubectl scale deployment hello-world --replicas=3`

    This will increase the number of replicas to three.

1. Verify that the deployment has been scaled by running the command below:

    `kubectl get deployment`

    This should display the `hello-world` deployment with three replicas.

## Conclusion

In this guide, we have shown you how to set up Kubernetes on your local development system using Minikube. We have also demonstrated how to deploy a simple web application and scale it easily using Kubernetes. With this knowledge, you can start experimenting with Kubernetes and develop applications that can be deployed in a production environment.

