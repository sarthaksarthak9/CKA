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


### Lab RBAC

Q1. Inspect the environment and identify the authorization modes configured on the cluster.<br>
- Check the kube-apiserver settings <br>

Q8. A user dev-user is created. User's details have been added to the kubeconfig file. Inspect the permissions granted to the user. Check if the user can list pods in the default namespace.<br>
- Use the --as dev-user option with kubectl to run commands as the dev-user.<br>

### Lab Service Account

Q13. You shouldn't have to copy and paste the token each time. The Dashboard application is programmed to read token from the secret mount location. However currently, the default service account is mounted. Update the deployment to use the newly created ServiceAccount

- Run the command kubectl describe pod and look for volume mount path.
- kubectl create serviceaccount dashboard-sa
- If you are interested checkout the files used to configure RBAC at /var/rbac

## Image security
- Edit deployment using kubectl edit deploy web command and add imagePullSecrets section. Use private-reg-cred.

Q5. Create a secret object with the credentials required to access the registry.
Name: private-reg-cred
Username: dock_user
Password: dock_password
Server: myprivateregistry.com:5000
Email: dock_user@myprivateregistry.com

- For q5 attempt this question using imperative commands

## Security Context

- Run the command: kubectl exec ubuntu-sleeper -- whoami and check the user that is running the container.
- To give user ID : 

```
apiVersion: v1
kind: Pod
metadata:
  name: ubuntu-sleeper
spec:
  securityContext:
    runAsUser: 1010   # Set at pod level (already present)
  containers:
  - name: ubuntu
    image: ubuntu
    command: ["sleep", "4800"]
    securityContext:
      runAsUser: 1010   # Explicitly set at container level

```

### Network Policy

Q10 attempt it again