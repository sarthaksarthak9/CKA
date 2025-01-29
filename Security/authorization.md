## Authorization Mechanisms
- node
- ABAC (Attribute Based Access Control)
- RBAC (Role Based Access Control)
- Webhook
- Always allow
- Always deny


### RBAC (Role Based Access Control)

##### Each role has 3 sections

- apiGroups: for core groups we can leave it empty or for any other group we can specify the group name
- resources: resources to which the role has access
- verbs: action that can be performed on the resources

```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: developer
rules:
- apiGroups: [""] # "" indicates the core API group
  resources: ["pods"]
  verbs: ["get", "list", "update", "delete", "create"]
- apiGroups: [""]
  resources: ["ConfigMap"]
  verbs: ["create"]
```

##### The next step is to link the user to that role

For this we create another object called RoleBinding. This role binding object links a user object to a role. <br>

```
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: devuser-developer-binding
subjects:
- kind: User
  name: dev-user # "name" is case sensitive
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: developer
  apiGroup: rbac.authorization.k8s.io
```

## Resource Name 

```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: developer
rules:
- apiGroups: [""] # "" indicates the core API group
  resources: ["pods"]
  verbs: ["get", "update", "create"]
  resourceNames: ["blue", "orange"]
```
