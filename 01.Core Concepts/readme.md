### Create pod imperative
>kubectl run nginx --image=nginx

### Create yaml file pod declarative
>kubectl run nginx --image=nginx --dry-run=client -o yaml

apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
spec:
  containers:
  - image: nginx
    name: nginx
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}

### Edit Pod Command
>kubectl edit pod nginx

### Edit Pod Recreate
>kubectl get pod nginx -o yaml /tmp/my-pod.yaml
>kubectl delete nginx 
>kubectl apply -f /tmp/my-pod.yaml

### ReplicationController
>kubectl get replicationcontrollers

### ReplicaSet
>kubectl get replicasets

### Scale ReplicaSet
>kubectl scale --replicas=2 -f replicaset-definition.yaml
or
>kubectl scale --replicas=3 replicasets my-replicaset

### Deployments
