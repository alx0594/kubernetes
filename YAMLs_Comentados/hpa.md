# 📊 HPA - Horizontal Pod Autoscaler

## ✅ Conceito
Ajusta automaticamente o número de Pods com base no uso de CPU/memória ou métricas customizadas.

## 📄 Exemplo YAML
```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: meu-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: meu-deployment
  minReplicas: 2
  maxReplicas: 10
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 60
```
> 📈 Esse HPA ajusta as réplicas do Deployment entre 2 e 10 conforme o uso de CPU.
