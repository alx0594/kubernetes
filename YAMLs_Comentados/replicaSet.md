# ReplicaSet

---

- O ReplicaSet garante que sempre existam N réplicas de um Pod rodando.

- Se um Pod falhar ou for deletado, o ReplicaSet criará outro automaticamente.

- O selector deve casar com os labels definidos no template.metadata.labels.

- Normalmente, usa-se Deployment em vez de ReplicaSet diretamente, pois ele oferece mais funcionalidades (como rollout/rollback).

```yaml
apiVersion: apps/v1 # API utilizada para o recurso ReplicaSet (versão atual estável)
kind: ReplicaSet # Define o tipo de objeto como ReplicaSet
metadata:
  name: meu-replicaset # Nome identificador do ReplicaSet
  labels:
    app: minha-app # Rótulo aplicado ao ReplicaSet (útil para identificação e organização)

spec:
  replicas: 3 # Número desejado de Pods ativos simultaneamente
  selector: # Define como o ReplicaSet encontra os Pods que ele deve gerenciar
    matchLabels:
      app: minha-app # O ReplicaSet cuidará de Pods que tenham este rótulo
  template: # Template usado para criar novos Pods
    metadata:
      labels:
        app: minha-app # Os Pods criados terão este mesmo rótulo (deve combinar com o selector)
    spec:
      containers:
        - name: nginx # Nome do contêiner (interno ao Pod)
          image: nginx:1.25 # Imagem do contêiner usada para este Pod
          ports:
            - containerPort: 80 # Porta exposta no contêiner
```

## Explicação dos principais campos

- **apiVersion / kind**  
  Define que este recurso é um ReplicaSet e usa a API apps/v1.

- **metadata.name**  
  Identificador único dentro do namespace.

- **metadata.labels**  
  Labels anexados ao ReplicaSet, úteis para organização e seleção.

- **spec.replicas**  
  Quantidade desejada de réplicas de Pod.

- **spec.selector.matchLabels**  
  Critério que o ReplicaSet usa para gerenciar apenas os Pods com esses labels.

- **spec.template**  
  Template de Pod que será replicado; precisa conter os mesmos labels do selector.

- **template.metadata.labels**  
  Labels que marcam os Pods criados pelo ReplicaSet.

- **template.spec.containers**  
  Definição dos contêineres dentro dos Pods: imagem, portas, probes, etc.

- **readinessProbe**  
  Verifica se o contêiner está pronto para receber tráfego; antes disso, o Service não encaminha requisições para ele.

- **livenessProbe**  
  Verifica se o contêiner está vivo; falhas sucessivas fazem o kubelet reiniciar o contêiner.
