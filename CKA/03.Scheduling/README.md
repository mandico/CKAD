### 1. Manual Scheduling

Caso nao queira schedular manualmente um pod, basta definir a propriedade nodeName no manifesto.
``` yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: nginx
  name: nginx
spec:
  containers:
  - image: nginx
    name: nginx
  nodeName: node02
```

Se nao tiver um agendador, o pod permanece no estado de Pending.
Para agendar um pod já existente, se faz necessario criar um Binding via API:
``` yaml
apiVersion: v1
kind: Binding
metadata:
  name: nginx
target:
  apiVersion: v1
  kind: Node
  name: node02
```

``` bash
curl --header "Content-Type:application/json" --request POST --data '{"apiVersion":"v1", "kind":"Binding"...}'
http://$SERVER/api/v1/namespaces/default/pods/$PODNAME/binding/
```

---

### 2. Labels and Selectors

---

### 3. Taints and Tolerations

``` bash
kubectl taint nodes NODE_NAME key=value:taint-effect
### Example
kubectl taint nodes node01 app=blue:NoSchedule
```

``` yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
spec:
  containers:
  - image: nginx
    name: myapp-pod
  tolerations:
  - key: app
    operator: Equal
    value: blue
    effect: NoSchedule
```

---

### 4. NodeSelectors

Label Nodes:
``` bash
kubectl label nodes <node-name> <label-key>=<label-value>
### Example
kubectl label nodes node01 size=Large
```

``` yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
spec:
  containers:
  - image: nginx
    name: myapp-pod
  nodeSelector:
    size: Large
```

---

### 5. Node Affinity

``` yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
spec:
  containers:
  - image: nginx
    name: myapp-pod
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
          - matchExpressions:
              - key: size
                operator: In
                values:
                  - Large
                  - Medium
```

### 6. Resources Requeriments and Limits

``` yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    name: myapp-pod
spec:
  containers:
  - name: myapp-pod
    image: nginx
    resources:
      requests:
        memory: "128Mi"
        cpu: "250m"
      limits:
        memory: "254Mi"
        cpu: "500m"
```

### 7. Daemon Sets

A DaemonSet ensures that all (or some) Nodes run a copy of a Pod. As nodes are added to the cluster, Pods are added to them. As nodes are removed from the cluster, those Pods are garbage collected. Deleting a DaemonSet will clean up the Pods it created.

Some typical uses of a DaemonSet are:

- running a cluster storage daemon on every node
- running a logs collection daemon on every node
- running a node monitoring daemon on every node

``` yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: monitoring-daemon
spec:
  selector:
    matchLabels:
      app: monitoring-agent
  template:
    metadata:
      labels:
        app: monitoring-agent
    spec:
      containers:
      - name: monitoring-agent
        image: monitoring-agent
```

### 8. Static Pods

Kubelet
/etc/kubernetes/manifests

Static Pods:
- Created by the Kubelet.
- Deploy Control Pane components as Static Pods.
- Ignored by Kube-Scheduler.
Daemon Sets:
- Created by Kube-API server (DaemonSet Controller).
- Deploy Monitoring Agents, Logging Agents on Nodes.
- Ignored by Kube-Scheduler.

### 8. Multiple Schedules

``` yaml
apiVersion: kubescheduler.config.k8s.io/v1
kind: KubeSchedulerConfiguration
profile:
- scheduleName: my-scheduler
```