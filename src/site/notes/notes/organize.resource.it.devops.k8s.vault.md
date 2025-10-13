---
{"dg-publish":true,"permalink":"/notes/organize-resource-it-devops-k8s-vault/","title":"Vault"}
---


Способ управления секретами - Hashicorp Vault

## Инжект env переменных напрямую

<https://bank-vaults.dev/docs/mutating-webhook/configuration/>

banzaicloud/vault-operator - оператор для k8s

ENV переменные вставленные таким способом будут видны только процессу с PID = 1

```sh
cat /proc/1/environ
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
  labels:
    app: myapp
spec:
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
      annotations:
        vault.security.banzaicloud.io/vault-addr: "https://vault:8200"
        vault.security.banzaicloud.io/vault-tls-secret: vault-tls
        vault.security.banzaicloud.io/vault-role: default
    spec:
      containers:
      - name: myapp
        image: docker.elastic.co/myapp
        env:
          - name: MYPASSWORD
            value: 'vault:secret/data/myapp#MYPASSWORD'

```