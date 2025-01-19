## Encrypting secret data at rest 

Encrypting secret data at rest is a critical security practice that ensures sensitive information stored in databases, files, or other storage systems is protected from unauthorized access, even if the storage medium is compromised. This is especially important for secrets like passwords, API keys, certificates, and other confidential data.

**In the context of Kubernetes**, encrypting secret data at rest refers to encrypting the Secret objects stored in the etcd database (Kubernetes' key-value store). By default, Kubernetes stores Secret objects in etcd in base64-encoded form, which is not secure because base64 is not encryption—it’s just encoding. To enhance security, Kubernetes provides mechanisms to encrypt Secret data at rest.



```
apiVersion: apiserver.config.k8s.io/v1
kind: EncryptionConfiguration
resources:
  - resources:
      - secrets
    providers:      ## order matters a lot here if identify at top then it does not encrypt data.
      - aescbc:
          keys:
            - name: key1
              secret: <base64-encoded-encryption-key>
      - identity: {}  # Fallback provider (no encryption)
```