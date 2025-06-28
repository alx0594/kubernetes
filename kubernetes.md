# 📚 Fundamentos de Kuberntes

---

## 🎯 O que é o Kubernetes?

O **Kubernetes** é uma ferramenta de orquestração de containers.

- Open Source
- Altamente utilizado penas empresas.
- Gerencia todo ciclo de vida de um container

## 🛡️ Imutabilidade no Kubernetes

A **imutabilidade** é uma característica essencial no Kubernetes que promove a **alta disponibilidade** e a **resiliência** das aplicações. Em vez de modificar objetos existentes, o Kubernetes substitui-os por **novas versões**. Isso garante que:

- As **atualizações** (como novas imagens ou configurações) não causem indisponibilidade em produção.
- O estado anterior possa ser recuperado facilmente, permitindo **rollbacks seguros**.
- Cada alteração resulte em um **novo objeto ou versão**, mantendo o histórico de mudanças sob controle (ex: _ReplicaSet, Deployment_).

Esse comportamento está alinhado com os princípios de **infraestrutura imutável** e **automação contínua**, tornando os sistemas mais confiáveis e previsíveis em ambientes dinâmicos.
