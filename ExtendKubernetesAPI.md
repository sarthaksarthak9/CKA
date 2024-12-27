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


