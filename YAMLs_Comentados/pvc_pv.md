# 💾 PVC & PV

## ✅ Conceito
PV representa o recurso de armazenamento. PVC é a requisição de uso desse recurso.

## 📄 Exemplo PVC
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: meu-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

## 📄 Exemplo PV
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: meu-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
```
> 🧩 O PVC será vinculado ao PV compatível para persistência de dados.
