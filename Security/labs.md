### Lab Cert Details

Q2. Identify the Certificate file used to authenticate kube-apiserver as a client to ETCD Server.

- Run the command cat /etc/kubernetes/manifests/kube-apiserver.yaml and look for value of etcd-certfile flag. <br>

Q4. <br>

Q6. What is the Common Name (CN) configured on the Kube API Server Certificate?

- openssl x509 -in file-path.crt -text -noout


### Lab Certificate API

- kubectl certificate deny agent-smith
- kubectl certificate approve agent-smith

