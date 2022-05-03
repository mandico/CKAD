Components:
- Master
- Worker

- etcd:
    base de dados em formato de chave/valor, no qual armazena todas as configuracoes do cluster (Nodes, Pods, Configs, Secrets, Accounts, Roles, Bindings, Others).
    Porta Padrao: 2379.

- kube-apiserver:

- kubelet:

- kube-proxy:

- kube-schedule:

- controller-manager
    - node-controller
    - replication-controller

- Container Runtime Engine