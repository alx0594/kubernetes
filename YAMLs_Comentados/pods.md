# 📦 Pod

## ✅ Conceito
Um Pod é a menor unidade implantável no Kubernetes, encapsulando um ou mais contêineres que compartilham rede e armazenamento.

## 📄 Exemplo YAML
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: meu-pod
spec:
  containers:
    - name: nginx
      image: nginx:1.25
```
> 🎯 Esse YAML define um Pod chamado `meu-pod` com um contêiner Nginx.
