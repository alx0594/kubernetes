# 🔒 Secret

## ✅ Conceito
Armazena informações sensíveis como senhas e tokens, codificadas em base64.

## 📄 Exemplo YAML
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: exemplo-secret
type: Opaque
data:
  password: c2VuaGExMjM=  # senha codificada em base64
```

## 🎯 Uso no Pod
```yaml
env:
  - name: DB_PASSWORD
    valueFrom:
      secretKeyRef:
        name: exemplo-secret
        key: password
```
> 🔐 Os valores do Secret são acessíveis com segurança via variáveis de ambiente.
