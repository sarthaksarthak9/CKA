- TLS encryption
- Kubernetes does not manage user accound natively
- All user manage by kube-api server
- private key extension (.key, key.pem) and public key extension (.crt, .pem)
- kube-api server only component talks to etcd. And it monior cluster via kubelet. So it use same certificate to authenticate itself to etcd and kubelet.

### Way to authenticate

- Static password file
- Static token file 
- Certificates
- Identity servers (third party solutions)

### Learn how encryption and decryption works

### How does browser knows certificated signed by a valid CA?

- Browser has a list of trusted CA. CA signs the certificate using private key and browser has public key inbuilt to checks if the CA is in the list of trusted CA.

### Understand what is PKI(public key infrastructure)
PKi is a set of roles, policies, and procedures needed to create, manage, distribute, use, store, and revoke digital certificates and manage public-key encryption.

## TLS in Kubernetes

#### We need to make two types of decisions.
- Who can access?
- What can they do?

Three certificats: <br>
- CA certificate
- Server certificate
- Client certificate

<br>

Client access the kubernetes cluster through kubectl utility. So, while accessing the cluster, the client needs to authenticate itself to the server. The server authenticates the client using the client certificate. The client certificate is signed by the CA certificate. The server has the CA certificate to verify the client certificate. The client has the server certificate to verify the server.

<br>

Two requirements:
- The client needs to have the client certificate and key
- All service within the cluster needs to have the server certificate and key

<br>





