## Extend kubernetes APIs

There are two primary ways to extend the Kubernetes API:

1. Custom Resources 2. Aggregation Layer

### Custom Resources

Custom Resources(CR) allow you to define your own resource types in kubernetes. The resources can be managed by using kubernetes tools (eg. ** kubectl **) and APIs as build in resources. CRs are typically used to define domain-specific objects or configurations

Example: Creating a Custom Resource

Suppose you want to create a custom resource called Book to manage books in a library application.

Step 1: Define a Custom Resource Definition (CRD)
A Custom Resource Definition (CRD) is a YAML file that defines the schema for your custom resource.

```
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: books.library.example.com
spec:
  group: library.example.com
  versions:
    - name: v1
      served: true
      storage: true
      schema:
        openAPIV3Schema:
          type: object
          properties:
            spec:
              type: object
              properties:
                title:
                  type: string
                author:
                  type: string
                isbn:
                  type: string
  scope: Namespaced
  names:
    plural: books
    singular: book
    kind: Book
    shortNames:
      - bk     
```
- group: The API group for the custom resource (library.example.com).
- versions: The API version (v1).
- schema: Defines the structure of the custom resource (e.g., title, author, isbn).
- scope: Specifies whether the resource is namespaced or cluster-scoped.
- names: Defines the plural, singular, and short names for the resource.

Step 2: Create an Instance of the Custom Resource
Now, you can create a Book resource:
```
apiVersion: library.example.com/v1
kind: Book
metadata:
  name: kubernetes-in-action
spec:
  title: Kubernetes in Action
  author: Marko Luksa
  isbn: 9781617293726
```

Step 3: Manage the Custom Resource
You can now manage the Book resource using kubectl:

** kubectl get books **
** kubectl describe book kubernetes-in-action **

2. Agrregation Layer
It allows you to extend kubernets API by deploying additional APIservers. These API servers can handle custom logic and resources, and they are integrated into the main kubernetes API server

Example: Extending the API with an Aggregation Layer
Suppose you want to add a custom API for managing Cars in a cluster.

Step 1: Deploy a Custom API Server
Create a custom API server that handles Cars resources. For example, you might write a server in Go that exposes endpoints like /apis/cars.example.com/v1/cars.

Step 2: Register the Custom API Server with Kubernetes
To integrate the custom API server with Kubernetes, you need to create an APIService resource:
```
apiVersion: apiregistration.k8s.io/v1
kind: APIService
metadata:
  name: v1.cars.example.com
spec:
  service:
    name: car-api-service
    namespace: default
  group: cars.example.com
  version: v1
  insecureSkipTLSVerify: true
  groupPriorityMinimum: 1000
  versionPriority: 15
```
- service: Specifies the Kubernetes service that exposes the custom API server.
- group: The API group for the custom resource (cars.example.com).
- version: The API version (v1).

Step 3: Use the Custom API
Once the custom API server is registered, you can interact with it using kubectl or direct API calls. For example:
```
kubectl get cars
```

## When to use Each Method

- Custom Resources: Use CRDs when you need to define new resources types with simple schemas and no custom logic.
- Aggregation Layer: Use the Aggregation Layer when you need advanced functionality, custom logic, or integration with external systems.




