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