## 🫛 Pods

### Criando pods imperativamente

- kubectl get pods
- kubectl get pods --all-namespaces
- kubectl run my-pod-apache-server --image httpd
- kubectl get pods -o wide
- kubectl delete pod my-pod-apache-server (Como só existe o manifesto do pod, o mesmo é excluído permanentemente)

### Criando pods usando manifesto

- kubectl apply -f pod.yaml
- kubectl delete pod my-pod-webserver
- kubectl delete --all pods && kubectl get pods
- watch kubectl get pods

Quando deletamos um pod e ele é recriado, o replicaSet que está garantindo que esse pod seja recriado.

---

## 🔁 ReplicaSets

- kubectl get replicaset
- kubectl apply -f Udemy/replicaSet.yaml
- kubectl delete replicaset frontend-rs

**Editando de forma imperativa**

- kubectl scale replicasets frontend-rs --replicas=5

Ao excluir o replicaset, todos os pods que ele estava controlando são deletados.

Manipulamos a quantidade de replicas, fazemos o apply e Kubernetes se encarrega de aplicar as replicas especificadas no yaml.

---

## 🏗️ Deployment

- Faz a implantação da aplicação
- Usa estratégia Rolling Update como default. (default 25% de indispinibilidade dos pods)
- Outra estratégia Recreate Deployment (Causa indisponibilidade)
- Rollback

- Deployment cria tanto o pod quanto o replicaset

**Comandos**

- kubectl apply -f Udemy/deployment.yaml
- kubectl rollout status deployment.apps/frotend-deployment
- kubectl describe deployment frontend-deployment
