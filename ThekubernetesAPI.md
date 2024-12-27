## Introduction

1. Kubernetes API is the central interface fir queing and manipultaing the state of obj in a kubernetes cluster
2. The API is exposed to api server which provide http API for managing kubernetes object like pod, namespace, cpnfigmaps and events

## Discovery
/api, /apis

## OpenAPI interface 
/openapi/v3

## Protobuf Serialization
kubernetes support the protobuf serialization for intra-cluster communication, offering and alter to JSON.

## Persistance
The state of kubernetes object is stored in **etcd**, a distributed key-value store.

## API Groups and Versioning:

- Kubernetes supports multiple API versions to facilitate evolution and deprecation of fields or resources.

- API resources are distinguished by their group, type, namespace (for namespaced resources), and name.

- The API server handles version conversion transparently, allowing objects to be accessed and modified across different API versions.

## API Extension

- Kubernetes api can be extebded using:
  ** 1. Custom Resource: ** Declaratively define new resource APIs.
  ** 2. Aggregation Layer: ** Implement additional api servers to extend functionality.

## Key Points:

1. The Kubernetes API is the backbone of cluster management, enabling interaction with cluster objects.

2. It supports multiple access methods, including command-line tools, REST calls, and client libraries.

3. API specifications are published via the Discovery API and OpenAPI documents, with OpenAPI v3.0 being the preferred standard.

4. Kubernetes ensures backward compatibility for GA APIs, while beta and alpha APIs require careful management during upgrades.

5. The API can be extended using custom resources or an aggregation layer to meet specific use cases.
