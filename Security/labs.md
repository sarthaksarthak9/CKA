### Lab Cert Details

Q2. Identify the Certificate file used to authenticate kube-apiserver as a client to ETCD Server.

- Run the command `cat /etc/kubernetes/manifests/kube-apiserver.yaml` and look for value of etcd-certfile flag. <br>

Q4. <br>

Q6. What is the Common Name (CN) configured on the Kube API Server Certificate?

- openssl x509 -in file-path.crt -text -noout

### Lab Certificate API

- kubectl certificate deny agent-smith
- kubectl certificate approve agent-smith


### Lab KubeConfig

Q2. To view config file - `k config view` <br>

Q12. To change context in a kubeconfig file - `k config --kubeconfig=/root/my-kube-config use-context research` <br>

Q13. 

- Add the my-kube-config file to the KUBECONFIG environment variable. <br>
- Open your shell configuration file: `vi ~/.bashrc` <br>
- Add the following line to export the variable: `export KUBECONFIG=/root/my-kube-config` <br>
- Apply the Changes: <br>
- Reload the shell configuration to apply the changes in the current session: `source ~/.bashrc`


