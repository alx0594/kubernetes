# 📡 Service

## ✅ Conceito
Expõe Pods para comunicação interna ou externa, criando uma camada de rede estável.

## 📄 Exemplo YAML
```yaml
apiVersion: v1
kind: Service
metadata:
  name: meu-service
spec:
  selector:
    app: minha-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: ClusterIP
```
> 🌐 Esse YAML expõe os Pods com `app=minha-app` na porta 80 internamente no cluster.
