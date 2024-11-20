# Task Detail
The Nautilus DevOps team is planning to deploy some micro services on Kubernetes platform. The team has already set up a Kubernetes cluster and now they want to set up some namespaces, deployments etc. Based on the current requirements, the team has shared some details as below:

Create a namespace named dev and deploy a POD within it. Name the pod dev-nginx-pod and use the nginx image with the latest tag. Ensure to specify the tag as nginx:latest.

Note: The kubectl utility on jump_host is configured to operate with the Kubernetes cluster.

# Solution

Create manifest file for bamespace creation my-namespace.yaml

```
apiVersion: v1
kind: Namespace
metadata:
  name: <insert-namespace-name-here>
```

Create manifest file for pod creation pod.yml

```
apiVersion: v1
kind: Pod
metadata:
  name: dev-nginx-pod
spec:
  containers:
  - name: nginx
    image: nginx:latest
   
```
Run below command to create namespace and pod.

```
kubectl get namespace
kubectl create namespace <insert-namespace-name-here> or kubectl create -f ./my-namespace.yaml
kubectl apply -f pod.yml
kubetctl get pod -n=dev
```

Reference: 

https://kubernetes.io/docs/tasks/administer-cluster/namespaces/#creating-a-new-namespace
https://kubernetes.io/docs/concepts/workloads/pods/
