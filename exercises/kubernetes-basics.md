# Exercise: Getting Started with Kubernetes
In this exercise, we will learn the fundamentals of Kubernetes, an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications. Kubernetes provides a robust and flexible infrastructure for running distributed systems and microservices.

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
