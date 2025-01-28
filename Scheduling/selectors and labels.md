## Pod
```
apiVersion: v1
kind: Pod
metadata:
    name: simple-webapp
    labels:
        app: app-1
        function: frontend
spec:
    containers:
    -   name: simple-webapp
        image: nginx
        ports:
        - containerPort: 8080
```
## ReplicaSet

```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
    name: simple-webapp
    labels:
        app: App1
        function: Front-end
spec:
    replicas: 3
    selector:
        matchLabels:
            app: App1
    template:
        metadata:
            labels:
                app: App1
                function: Front-end
        spec:
            containers:
            -   name: simple-webapp
                image: simple-webapp
```

## Service

```
apiVersion: v1
kind: Service
metadata:
    name: svc-1
spec:
    selector:
        app: app1
    ports:
    -   protocol: TCP
        port: 80
        targetPort: 9376
```