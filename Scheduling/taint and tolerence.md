## Taint and Tolerence

- Taints are set on nodes
- Tolerence are set on pod

Taints and Toleration does not tell pod to go to particular node. Instead, it tells node to only accept pod with certain tolerations.


```
apiVersion: v1
kind: Pod
metadata:
    name: web-app1
spec:
    containers:
    - name: web-app1
      image: web-app1
    tolerations:
    - key: "app"
      operator: "Equal"
      value: "blue"
      effect: "NoSchedule"
```

# Taint Effects

There are three types of taint effects:

## 1. NoSchedule

**Behavior:**

- Pods that do not tolerate the taint will not be scheduled on the node.
- Existing Pods on the node are not affected.

**When to Use:**

Use this when you want to reserve a node for specific Pods (e.g., production workloads).

**Example:** Taint a node for GPU workloads and only allow GPU-enabled Pods to run on it.

---

## 2. PreferNoSchedule

**Behavior:**

- Kubernetes will try to avoid scheduling Pods that do not tolerate the taint on the node.
- However, if no other nodes are available, the Pod may still be scheduled on the tainted node.

**When to Use:**

Use this when you want to prefer certain nodes for specific Pods but still allow scheduling on other nodes if necessary.

**Example:** Prefer nodes in a specific availability zone but allow scheduling elsewhere if needed.

---

## 3. NoExecute

**Behavior:**

- Pods that do not tolerate the taint will not be scheduled on the node.
- Existing Pods on the node that do not tolerate the taint will be evicted.

**When to Use:**

Use this when you want to evict existing Pods that do not tolerate the taint.

**Example:** Taint a node for maintenance and evict all non-critical Pods.