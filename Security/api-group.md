## API Groups

The kubernetes API is grouped into several groups(/version, /api, etc). Each group is responsible for a set of resources (/health, /metrics, etc). 

API groups are used to organize the Kubernetes API. The API group is specified in a REST path and in the `apiVersion` field of a Kubernetes object. The API group is the first path segment in the URL, afteqr the `/apis/`. For example, in the API path `/apis/apps/v1/namespaces/default/deployments/my-deployment`, the API group is `apps`.

#### These APIs are catagorized into two.

1. The core group - Where all the functionality exists

core:- /api--->/v1----> (/namespaces, /pods, /rc, etc) see notes

2. The named group - More organized and going forward all the newer features are going to be made available to these named groups.<br>

named:- /apis--->/group/version{These are API groups}----> (/apps, /batch, /extensions, etc){These are resources} see notes

`Access kube-API server at port 6443 without any path`(we can see every available api group) <br>

```
curl http://whatever:6443 -k 
```

```
curl http://whatever:6443 -k | grep "nameofresource"
```

To access all the resource groups pass certificate and key to the curl command.<br>
Alternate, to launch kube proxy service on port 8001 & use certificates and cerendials from the kubeconfig file.<br>

#### kube Proxy and kubectl proxy

`kube proxy:` It is used to enable connectivity between pods and svc across different nodes <br>

`kubectl proxy:` It is used to access the kubernetes API server from the local machine. It creates a proxy server between the local machine and the kubernetes API server. <br>


