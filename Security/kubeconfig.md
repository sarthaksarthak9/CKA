## Kubeconfig

To store the configuration of the Kubernetes cluster, the kubeconfig file is used. This file is created automatically when the cluster is created. The kubeconfig file is stored in the .kube directory in the user's home directory. 

#### The kubeconfig file has 3 sections

- Clusters: This section contains the details of the cluster. Server specification and in commands goes here

- Contexts: it defines which user have which cluster access permissions. It also defines the default cluster and user.

- Users: admin keys and certificates are stored in this section.

```
apiVersion: v1
kind: Config
preferences: {}

clusters:
- name: development
  cluster:
    server: https://dev.example.com
    certificate-authority: /path/to/dev-ca.crt
- name: test
  cluster:
    server: https://test.example.com
    certificate-authority: /path/to/test-ca.crt

users:
- name: developer
  user:
    client-certificate: /path/to/developer.crt
    client-key: /path/to/developer.key
- name: experimenter
  user:
    client-certificate: /path/to/experimenter.crt
    client-key: /path/to/experimenter.key

contexts:
- name: dev-frontend
  context:
    cluster: development
    user: developer
    namespace: frontend
- name: dev-storage
  context:
    cluster: development
    user: developer
    namespace: storage
- name: exp-test
  context:
    cluster: test
    user: experimenter
    namespace: default

current-context: dev-frontend

```