### Certificate Authority (CA)

Generate Keys
```
$ openssl genrsa -out ca.key 2048
```
Generate CSR
```
$ openssl req -new -key ca.key -subj "/CN=KUBERNETES-CA" -out ca.csr
```
Sign certificates
```
$ openssl x509 -req -in ca.csr -signkey ca.key -out ca.crt
```

#### Why Self-Signed Certificates?
In private networks (e.g., Kubernetes), you don't need a public CA. Instead, you create your own private CA and use it to sign certificates for your components. This is more efficient and cost-effective for internal use.

#### To identify user as admin or normal

```
/CN=kube-admin/O=system:masters 
```

We can use this certificates instead passing username and password in a rest api calls and specify them in kube.config file


### Server side Cert

#### ETCD 

High avilable env so required additional peer certificate

#### kube-api 

API Client cert use by api server while communication as a client to ETCD and kubelet server

#### kubelet Server

kubelet use client cert to authenticate into kube-api server. The API-Server needs to know which node is authenticating and give the right set of information. Therefore, it is important node to have right name in right order





