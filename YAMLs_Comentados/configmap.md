# ⚙️ ConfigMap

## ✅ Conceito
Armazena dados de configuração não sensíveis que podem ser injetados em Pods.

## 📄 Exemplo YAML
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: exemplo-config
data:
  APP_MODE: "dev"
  TIMEOUT: "30"
```

## 🎯 Uso no Pod
```yaml
env:
  - name: APP_MODE
    valueFrom:
      configMapKeyRef:
        name: exemplo-config
        key: APP_MODE
```
> 🧩 Esse exemplo injeta as variáveis de ambiente a partir do ConfigMap.
