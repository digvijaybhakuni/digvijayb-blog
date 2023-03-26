---
layout: post
title: Setup KIND with Docker for kubernetes development.
author: digvijayb
tags:
  - kubernetes
  - docker
  - KIND
date: 2023-03-26T09:59:42.780Z
description: Kubernetes is a popular container orchestration platform that allows users to deploy, manage, and scale containerized applications. Setting up a Kubernetes cluster on your local development system is a great way to learn the basics of Kubernetes and experiment with your applications. In this blog post, we will guide you through the process of setting up a Kubernetes cluster on your local development system using KIND (Kubernetes in Docker).
thumbnail: /images/uploads/featured.png
---
Kubernetes is a popular container orchestration platform that allows users to deploy, manage, and scale containerized applications. Setting up a Kubernetes cluster on your local development system is a great way to learn the basics of Kubernetes and experiment with your applications. In this blog post, we will guide you through the process of setting up a Kubernetes cluster on your local development system using KIND (Kubernetes in Docker).

<!-- more -->

### Step 1: Install Docker and KIND
Before installing KIND, you need to have Docker installed on your local system. You can download Docker for your operating system from the official Docker website. After installing Docker, you can then install KIND by following the instructions on the KIND GitHub repository.

### Step 2: Create a KIND Cluster
After installing KIND, you can create a Kubernetes cluster by running the following command:

`kind create cluster`

This command creates a new Kubernetes cluster using Docker containers as nodes. By default, KIND will create a single node cluster with the latest version of Kubernetes. You can customize the cluster by specifying additional options such as the number of nodes, Kubernetes version, and more.

### Step 3: Configure Kubectl
After creating the Kubernetes cluster, you need to configure kubectl, the Kubernetes command-line tool, to interact with the cluster. You can do this by running the following command:

`export KUBECONFIG="$(kind get kubeconfig-path --name="kind")"`

This command sets the KUBECONFIG environment variable to the path of the kubeconfig file for the KIND cluster.

### Step 4: Verify Cluster Setup
You can verify that the Kubernetes cluster is running by running the following command:

`kubectl cluster-info`

This command displays information about the Kubernetes cluster, such as the API server endpoint and the Kubernetes version.

### Step 5: Deploy an Application
Now that you have a running Kubernetes cluster on your local development system, you can deploy your first application to the cluster. In this example, we will deploy a simple web application using a Docker container.

1. Create a deployment by running the command below:

    `kubectl create deployment hello-world --image=gcr.io/google-samples/hello-app:1.0`

    This will create a deployment named `hello-world` with a single replica running the `hello-app` container image.

1. Expose the deployment by running the command below:

    `kubectl expose deployment hello-world --type=NodePort --port=8080`

    This will create a service that exposes the deployment to the external network.

1. Get the URL of the application by running the command below:

    `kubectl get service hello-world -o jsonpath='{.status.loadBalancer.ingress[0].ip}:{.spec.ports[0].nodePort}'`

    This should display the URL of the application that you can access from your web browser.

### Step 6: Scale the Application
One of the benefits of Kubernetes is the ability to scale applications easily. In this step, we will scale the `hello-world` deployment to three replicas.

1. Scale the deployment by running the command below:

    `kubectl scale deployment hello-world --replicas=3`

    This will increase the number of replicas to three.

1. Verify that the deployment has been scaled by running the command below:

    `kubectl get deployment`

    This should display the `hello-world` deployment with three replicas.

## Conclusion

In this guide, we have shown you how to set up a Kubernetes cluster on your local development system using KIND. We have also demonstrated how to deploy a simple web application and scale it easily using Kubernetes. With this knowledge, you can start experimenting with Kubernetes and develop applications that can be deployed in a production environment.