# Task Detail
The Nautilus DevOps team is diving into Kubernetes for application management. One team member has a task to create a pod according to the details below:

Create a pod named pod-httpd using the httpd image with the latest tag. Ensure to specify the tag as httpd:latest.

Set the app label to httpd_app, and name the container as httpd-container.

Note: The kubectl utility on jump_host is configured to operate with the Kubernetes cluster.

# Solution:


Create manifest file for pod creation pod-httpd.yml

```
apiVersion: v1
kind: Pod
metadata:
  name: pod-httpd
  labels:
    app: httpd_app
spec:
  containers:
  - name: httpd-container
    image: httpd:latest
```

Run below command to run pod and check pod details.
```
kubectl get pod
kubetctl apply -f pod-httpd.yml
kubectl get pod
kubectl describe pod pod-httpd
```
