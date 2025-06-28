# 🌐 Ingress

## ✅ Conceito
Gerencia o acesso HTTP externo aos serviços do cluster com base em regras de roteamento.

## 📄 Exemplo YAML
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: meu-ingress
spec:
  rules:
    - host: minhaapp.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: meu-service
                port:
                  number: 80
```
> 🌍 Esse Ingress roteia o tráfego para `meu-service` ao acessar `minhaapp.com/`.
