Components:
- Master
- Worker

- etcd:
    base de dados em formato de chave/valor, no qual armazena todas as configuracoes do cluster (Nodes, Pods, Configs, Secrets, Accounts, Roles, Bindings, Others).
    Porta Padrao: 2379.

- kube-apiserver:
    Eh responsavel por autenticar e validar solicitacoes, recuperar e atualizar dados no ETCD.

- kubelet:
    Eh o capitao do navio. Ele carrega ou descarrega os containers no navio conforme as instrucoes do kube-schedule.

- kube-proxy:
    Eh um processo que eh executado em cada no no cluster kubernetes.
    Seu trabalho eh procurar novos sercos e toda vez que um novo servico eh criado ele cria as regras apropriadas em cada no para encaminhar o trafego desses servicos para os pods de backend.

- kube-schedule:
    Responsavel pelo agendamento de pods nos nos. Responsavel apenas por decidir qual pod continua em qual no.

- kube-controller-manager
    - node-controller: responsavel por monitorar o status dos nos e executar as acoes necessarias para manter o aplicativo em execucao.
    - replication-controller: responsavel por monitorar o status dos conjuntos de replicas e garantir o numero desejado de PODs esteja disponivel o tempo todo dentro do conjunto. Se um pod morre, ele recria.

- Container Runtime Engine