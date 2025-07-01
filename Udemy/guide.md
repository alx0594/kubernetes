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
- kubectl rollout history deployment.apps/frontend-deployment
- kubectl describe deployment frontend-deployment
- kubectl describe deployment frontend-deployment | grep StrategyType

### Estratégias de deploy `RollingUpdate`

A estratégia `RollingUpdate` permite que atualizações sejam feitas gradualmente, sem indisponibilizar toda aplicação.

- `maxUnavailable: 25%`: Durante o update, **até 25% dos pods podem ficar indisponíveis** temporariamente.
  👉 Se você possui **4 pods, até 1 pod** pode ser derrubado por vez para atualização `(25% de 4 = 1)`

- `maxSurge: 25%`: Durante o update, o Kubernetes pode criar **até 25% de pods extras**, além do número desejado de réplicas.  
  👉 Com **4 pods definidos**, o cluster pode subir **1 pod extra** durante a atualização `(25% de 4 = 1)`, totalizando temporariamente **5 pods**

**📌 Resumo com 4 réplicas:**

- Até **1 pod pode estar fora do ar** duarante o update `(maxUnavailable)`
- Até **1 pod extra pode ser criado**, somando até **5 pods simultaneamente** `(maxSurge)`
- Esses pod extra **não estará indisponível**, mas sim **em fase de preparação** (como `Pending`, `ContainerCreating`, etc.) até se tornar `Ready`

### Rollout status e Rollout history

```bash
kubectl rollout status deployment/frontend-deployment
```

Verificando o histórico de revisões de um Deployment

O comando abaixo exibe o histórico de revisões do Deployment `frontend-deployment`

```bash
kubectl rollout history deployment/frontend-deployment
```

Cada revisão **_REVISION_** representa uma modificação relevante no Deployment. Vale destacar que **alterar apenas quantidade de réplicas** e reaplicar o manifest **não gera uma nova revisão**, pois o Kubernetes não considera isso uma mudança estrutural na especificação do Deployment.  
Por outro lado, **alterar a imagem do container** (por exemplo, modificando a tag da imagem) **gera uma nova revisão**, pois o Kubernetes entende que isso altera o comportamento da aplicação. Esse mecanismo é semelhante ao controle de versões em sistemas como o Git, em que cada alteração relevante cria um novo "commit"

- Verificar rollout de uma versão específica
  `kubectl rollout history deployment/frontend-deployment --revision=2`

**Rollback**

O comando abaixo executa o rollback para revision anterior:

```bash
kubectl rollout undo deployment/frontend-deployment
```

O comando a seguir executa o rollback de uma revision específica:

```bash
kubectl rollout undo deployment/frontend-deployment --to-revision=5
```

**Rollout Pause e Rollout Resume**

O comando abaixo pausa uma atualização:

```bash
kubectl rollout pause deployment/frontend-deployment
```

O comando **resume** faz par com o comando **pause**, dando continuidade na atualização que foi temporariamente interrompida.

```bash
kubectl rollout resume deployment/frontend-deployment
```

### Scale Up e Scale Down

- **Up**

```bash
kubectl scale deployment/frontend-deployment --replicas=11
```

- **Down**

```bash
kubectl scale deployment/frontend-deployment --replicas=11
```

### Estratégias de deploy `Recreate`

Lembrando que a estratégia default do Kubernetes é a **_RollingUpdate_**

- Alterar o tipo de estratégia dentro da **spec** no deployment.yaml

```yaml
strategy:
  type: Recreate
```

---

## 🛜 Kubernetes Networking

- Container to Container
- Pod to Pod Intra Node.
- Pod to Pod Inter Node.
  O Kubernetes provê uma rede virtual plana dentro do cluster, garantindo que todos os pods possam se comunicar entre si de forma transparente, independentemente de estarem em worker nodes on-premises ou em ambientes de nuvem pública, como AWS ou Azure, desde que estejam integrados ao mesmo cluster.

**Exercício**

- Criar yamls de pods do tomcat e redis.
- Descrever o pod do redis em busca do IP: `kubectl describe pod | grep IP`
- No pod do tomcat, instalar pacote de redes para teste de ping: `apt update -y && apt install iputils-ping`
- Entrar no pod do tomcat: `kubectl exec -it tomcat-pod -- bash`
- Por fim, executar o ping para o IP do pod do redis: `ping <ip-redis>`
