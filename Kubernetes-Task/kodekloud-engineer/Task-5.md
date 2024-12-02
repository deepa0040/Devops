# Task Details
An application currently running on the Kubernetes cluster employs the nginx web server. The Nautilus application development team has introduced some recent changes that need deployment. They've crafted an image nginx:1.17 with the latest updates.

Execute a rolling update for this application, integrating the nginx:1.17 image. The deployment is named nginx-deployment.

Ensure all pods are operational post-update.

Note: The kubectl utility on jump_host is set up to operate with the Kubernetes cluster

# Solution

Run Below command to check the required information for rolling update.

```
kubectl get pods
kubectl get deployment
kubectl describe deployment
```
Run below command to update the nginx image

```
kubectl set image deployment/<deployment-name <container_name>=nginx:1.17
```

Check Rolling update status

```
kubectl rollout status deployment/nginx-deployment
kubectl describe deployment
```

Reference:

[kubectl describe deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#updating-a-deployment)
