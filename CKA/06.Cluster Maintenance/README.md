### 1. OS Upgrades

O tempo de espera para que um node volte online é conhecido como pod-eviction-timeout e é definido pelo controller manager.

Para casos de manutencao a maneira mais segura é drenar os workloads para outros nodes. Tecnicamente nao sao movidas, mas sim finalizadas graciosamente do nó e recriadas em outro nó.
``` bash
kubectl drain node_name
```

Para tornar o node programavel, que possa receber os workloads após a manutencao, se faz necessario habilitar o scheduler.
``` bash
kubectl uncordon node_name
```

Existe tambem a possibilidade de marcar um node como nao agendando, onde ele nao drena os pods, porem nao recebe nenhum outro workload novo.
``` bash
kubectl cordon node_name
```

### 2. Cluster Upgrade Process

``` bash
kubeadm upgrade plan

### Upgrade Master
# upgrade kubeadm
apt-get upgrade -y kubeadm=1.2.0-00

# upgrade master
kubeadm upgrade apply -n 1.2.0

# upgrade kubelet
apt-get upgrade -y kubelet=1.2.0-00
systemctl restart kubelet
kubectl get nodes

### Upgrade Nodes
kubectl drain node01
# upgrade kubeadm
apt-get upgrade -y kubeadm=1.2.0-00
# upgrade kubelet
apt-get upgrade -y kubelet=1.2.0-00
kubeadm upgrade node config --kubelet-version v1.2.0
systemctl restart  kubelet

kubectl uncordon node01
kubectl get nodes
```

### 3. Backup and Restore Methods

##### Resource Configuration
"Backup" de alguns grupos de recursos do cluster.
``` bash
kubectl get all --all-namespaces -o yaml > all-deploy-services.yaml
```

##### ETCD Cluster
Armazena informacoes sobre o estado no nosso cluster, todos os nós e todos os outros recursos criados dentro do cluster sao armazenados no etcd.

etcd.service
--data-dir=/var/lib/etcd

``` bash
ETCDCTL_API=3 etcdctl \
   snapshot save snapshot.db \
   --endpoints=https://localhost:23079 \
   --cacert=/etc/etcd/ca.crt \
   --cert=/etc/etcd/etcd-server.crt \
   --key=/etc/etcd/etcd-server.key

ETCDCTL_API=3 etcdctl \
   snapshot status snapshot.db

# Restore
service kube-apiserver stop

ETCDCTL_API=3 etcdctl \
   snapshot restore snapshot.db \
   --data-dir /var/lib/etcd-from-backup

etcd.service
--data-dir=/var/lib/etcd-from-backup

systemctl daemon-reload
service etcd restart
service kube-apiserver start
```