## View Cert Details

It is import to know how cluster has been set up

- The hard way
- Kubeadm

```
cat /etc/kubernetes/manifests/kube-apiserver.yaml
```

#### To see logs 
```
journalctl -u etcd.service -l
```

#### CA Server

- CA is just a pair of private key and certificate we have generated. Whoever gain access can sign any certificates for our kubernetes env. So we have to place them on a server that is fully secure. Now this server become our CA.

- If anyone need to signing the certificates, they need CA server root cert and private key. 