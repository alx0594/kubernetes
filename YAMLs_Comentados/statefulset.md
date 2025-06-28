# 🗃️ StatefulSet

## ✅ Conceito
Gerencia Pods com identidade persistente e estável (nome, rede e armazenamento fixos).

## 📄 Exemplo YAML
```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: meu-app
spec:
  selector:
    matchLabels:
      app: minhaapp
  serviceName: "meu-servico"
  replicas: 3
  template:
    metadata:
      labels:
        app: minhaapp
    spec:
      containers:
        - name: app
          image: minhaimagem:latest
          volumeMounts:
            - name: dados
              mountPath: /dados
  volumeClaimTemplates:
    - metadata:
        name: dados
      spec:
        accessModes: ["ReadWriteOnce"]
        resources:
          requests:
            storage: 1Gi
```
> 🗂️ Cada Pod (`meu-app-0`, `meu-app-1`, etc.) recebe seu volume persistente.
