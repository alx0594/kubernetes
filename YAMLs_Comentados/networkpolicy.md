# 🔐 NetworkPolicy

## ✅ Conceito
Controla o tráfego de rede entre Pods e/ou redes externas com base em rótulos.

## 📄 Exemplo YAML
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-all
spec:
  podSelector: {}
  policyTypes:
    - Ingress
```
> 🚫 Essa política bloqueia todo tráfego de entrada para todos os Pods no namespace.
