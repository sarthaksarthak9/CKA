## Yaml in Kuebernetes 

https://www.youtube.com/watch?v=1uFVr15xDGg&pp=ygUEeWFtbA%3D%3D


## Structure

All of these follow same structure. A kubernetes deployment file follows 4 top level fields.

1. API Version 2. kind 3. MetaData 4. Spec

**Kind**   **Version**
pod            v1
service        v1
ReplicaSet     apps/v1
Deployment     apps/v1

```
apiVersion: v1
kind: pod
metadata:
  name: myapp-pod
  labels:
    app: myPod
    type: front-end
spec:
  containers:
  -  name: nginx-container
     image: nginx
```
