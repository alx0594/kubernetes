# 🧱 Deployment

## ✅ Conceito
Gerencia réplicas de Pods e permite atualizações declarativas e rollbacks.

## 📄 Exemplo YAML
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: meu-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: minha-app
  template:
    metadata:
      labels:
        app: minha-app
    spec:
      containers:
        - name: nginx
          image: nginx:1.25
```
> 🔁 Esse YAML cria 3 réplicas do Pod rotuladas com `app=minha-app`.
