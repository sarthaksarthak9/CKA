## Cluster Roles

- when we talk about cluster roles, we are talking about roles that are not namespaced, they are cluster wide.

### Cluster Scoped Resources
- we don't have to specify a namespace when creating a cluster role, because they are cluster wide. Like - nodes, pv, pvc, storage classes, etc.

### To see resources
- k api-resources -n true
- k api-resources -n false

## Intro

- To authorise a user to access a cluster wide resource, we need to create a cluster role and cluster role binding. <br>
 
- kind: ClusterRole or kind: ClusterRoleBinding <br>

- Also, we can use cluster roles, bindings for ns. But, in this user get permissions of all pod across the cluster.


