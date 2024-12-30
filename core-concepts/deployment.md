The defination of deployment.yaml is similiar as replication.yaml

A Deployment is a higher-level abstraction that manages ReplicaSets and provides declarative updates for Pods.

It is designed to manage the deployment and scaling of applications.

### Purpose:

Deployments are used to define and manage the desired state of an application, including the number of replicas, update strategy, and rollback capabilities.

They provide a more user-friendly way to manage ReplicaSets and Pods.

### Lifecycle:

Deployments manage the lifecycle of ReplicaSets. When you update a Deployment, it creates a new ReplicaSet and scales it up while scaling down the old ReplicaSet.

Deployments ensure that the desired state of the application is maintained, even during updates.

### Updates:

Deployments support rolling updates and rollbacks, allowing you to update Pods with zero downtime and revert to a previous version if needed.

Example

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-deployment
spec:
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: my-app
        image: nginx
  replicas: 3
  selector:
    matchLabels:
      app: nginx
```





  
