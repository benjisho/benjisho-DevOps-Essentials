# Exercise: Getting Started with Kubernetes
In this exercise, we will learn the fundamentals of Kubernetes, an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications. Kubernetes provides a robust and flexible infrastructure for running distributed systems and microservices.

## Table of Contents

- [Step 1: Deploying Your First Pod](#step-1-deploying-your-first-pod)
- [Step 2: Deploying a Service](#step-2-deploying-a-service)
- [Step 3: Scaling the Application](#step-3-scaling-the-application)
- [Conclusion](#conclusion)
- [Advanced Exercise: Deploying a Multi-Container Application with Kubernetes](#advanced-exercise-deploying-a-multi-container-application-with-kubernetes)

## Prerequisites
Before you start this exercise, ensure that you have the following prerequisites:

- Kubernetes Cluster: Set up a Kubernetes cluster on your local machine using tools like Minikube or on a cloud provider like Google Kubernetes Engine (GKE), Amazon Elastic Kubernetes Service (EKS), or Azure Kubernetes Service (AKS).
- Kubernetes CLI (kubectl): Install the Kubernetes command-line tool (kubectl) and configure it to connect to your Kubernetes cluster.

## Step 1: Deploying Your First Pod
1. Open a terminal or command prompt.

2. Verify that kubectl is installed and configured correctly:
```
kubectl version
```
3. Deploy a simple pod using a YAML file. Create a file named pod.yaml and add the following content:
```
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: nginx-container
      image: nginx:latest
      ports:
        - containerPort: 80
```
4. Apply the configuration to create the pod:
```
kubectl apply -f pod.yaml
```
5. Verify that the pod is running:
```
kubectl get pods
```
6. Describe the pod to see more details:
```
kubectl describe pod my-pod
```
## Step 2: Deploying a Service
1. Create a service to expose the pod you deployed in the previous step. Create a file named service.yaml and add the following content:
```
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: nginx-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: NodePort
```
2. Apply the configuration to create the service:
```
kubectl apply -f service.yaml
```
3. Get the URL to access the service:
```
minikube service my-service --url
```
4. Open the provided URL in your web browser, and you should see the default Nginx page.

## Step 3: Scaling the Application
1. Scale the number of replicas for the pod to 3:
```
kubectl scale --replicas=3 pod my-pod
```
2. Verify that the pods are running and have different pod names:
```
kubectl get pods -o wide
```
## Conclusion
Congratulations! We've completed the Kubernetes basics exercise.
We've learned how to deploy a pod, create a service to expose the pod, and scale the application by increasing the number of replicas.

# Advanced Exercise: Deploying a Multi-Container Application with Kubernetes
In this advanced exercise, we will explore how to deploy a multi-container application using Kubernetes. We will use Kubernetes features like Deployments, Services, and Volumes to manage a group of interconnected containers.

## Prerequisites
- Before you start this advanced exercise, make sure you have completed the "Getting Started with Kubernetes" exercise.

## Step 1: Create a Multi-Container Application
1. Create a new directory for your multi-container application project.

2. Inside the project directory, create a file named app.yaml and add the following content:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: multi-container-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: multi-container-app
  template:
    metadata:
      labels:
        app: multi-container-app
    spec:
      containers:
        - name: nginx-container
          image: nginx:latest
          ports:
            - containerPort: 80
        - name: busybox-container
          image: busybox:latest
          command: ["sleep", "3600"]
      volumes:
        - name: shared-volume
          emptyDir: {}
---
apiVersion: v1
kind: Service
metadata:
  name: multi-container-service
spec:
  selector:
    app: multi-container-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: NodePort
```

3. Use the appropriate Kubernetes objects (Deployments, Services, Volumes, etc.) to define the multi-container application.

4. Apply the configuration to deploy the multi-container application:
```
kubectl apply -f app.yaml
```
## Step 2: Verify the Deployment
1. Verify that all the pods and services for your multi-container application are running:
```
kubectl get pods,svc
```
2. Get the URL to access the service:
```
minikube service multi-container-service --url
```
3. Access your multi-container application through the exposed service.
    - Option 1: Open the provided URL in your web browser.
    - Option 2: you can use curl or any web browser tool to access the service from the terminal:
      ```
      curl <URL>
      ```

## Step 3: Clean Up
1. Delete the resources created for the multi-container application:
```
kubectl delete -f app.yaml
```
2. To check the status of pods, you can use the following command:
```
kubectl get pods
```
> If the resources have been successfully deleted, you will not see any pods related to the multi-container application in the output.

3. Check the status of services, you can use the following command:
```
kubectl get services
```
> If the resources have been deleted, you will not see the service you created for the multi-container application in the output.

4. You can use the describe command to get more detailed information about a specific pod or service. For example:
```
kubectl describe pod <pod_name>
kubectl describe service <service_name>
```
> If the resources have been deleted, running these commands for the relevant pod and service will result in an error, indicating that the resource does not exist.

5. By checking the status of pods and services using the kubectl get and kubectl describe commands, you can verify that the resources created for the multi-container application have been successfully deleted from your Kubernetes cluster.

## Conclusion
Congratulations! We've completed the Kubernetes basics exercise and an advanced exercise for deploying a multi-container application with Kubernetes.
We've learned how to deploy a pod, create a service to expose the pod, and scale the application by increasing the number of replicas. Additionally, we explored more advanced concepts by deploying a multi-container application.
