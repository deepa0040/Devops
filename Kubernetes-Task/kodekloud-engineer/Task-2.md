# Task Detail
The Nautilus DevOps team is delving into Kubernetes for app management. One team member needs to create a deployment following these details:

Create a deployment named httpd to deploy the application httpd using the image httpd:latest (ensure to specify the tag)

Note: The kubectl utility on jump_host is set up to interact with the Kubernetes cluster.

# Solution
Create manifest file for pod creation Deployment-httpd.yml

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: httpd
  labels:
    app: httpd
spec:
  replicas: 3
  selector:
    matchLabels:
      app: httpd
  template:
    metadata:
      labels:
        app: httpd
    spec:
      containers:
      - name: httpd
        image: httpd:latest
```
Run below command to run Deployment and check Deployment details.
```
kubectl apply -f deployment.yaml
kubectl get deployment
kubectl describe deployment <deployment-name>
```
