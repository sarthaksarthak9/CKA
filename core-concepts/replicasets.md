## Replica-Sets / Replication Controller

It help to run multiple instances of a single pod. It make ensure that specied number of pod keep running at all time. It also help to maintain and divide load across multiple node as well as scale our application.

Replica set and Replication Controller are two different thing. The difference is that replica set require selector defination

###### replica-set is the new way to set up replication. 

### When to use a ReplicaSet
A ReplicaSet ensures that a specified number of pod replicas are running at any given time. However, a Deployment is a higher-level concept that manages ReplicaSets and provides declarative updates to Pods along with a lot of other useful features. Therefore, we recommend using Deployments instead of directly using ReplicaSets, unless you require custom update orchestration or don't require updates at all.

This actually means that you may never need to manipulate ReplicaSet objects: use a Deployment instead, and define your application in the spec section.

Example ReplicaSet
```
apiVersion: apps/v1    ## keep in mind apps/v1
kind: ReplicaSet
metadata:
  name: frontend
  labels:
    app: guestbook
    type: frontend
spec:
  # modify replicas according to your case
  template:
    metadata:
      labels:
        type: frontend
    spec:
      containers:
      - name: php-redis
        image: us-docker.pkg.dev/google-samples/containers/gke/gb-frontend:v5

  replicas: 3
  selector:
    matchLabels:
      type: frontend
```

Example Replication Controller

```
    apiVersion: v1
    kind: ReplicationController
    metadata:
      name: myapp-rc
      labels:
        app: myapp
        type: front-end
    spec:
     template:
        metadata:
          name: myapp-pod
          labels:
            app: myapp
            type: front-end
        spec:
         containers:
         - name: nginx-container
           image: nginx

     replicas: 3
```

