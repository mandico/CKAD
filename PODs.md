**Get All Pods**
```sh
$ kubectl get pods
```

-----------

**Create a new pod with the nginx image**
```sh
$ kubectl run nginx --image=nginx
```

-----------

**Check image in pod**
```sh
$ kubectl describe pod <<pod_name>>
```

-----------

**Which nodes are these pods placed on**
```sh
$ kubectl get pods -o wide
NAME            READY   STATUS    RESTARTS   AGE    IP           NODE           NOMINATED NODE   READINESS GATES
nginx           1/1     Running   0          2m6s   10.42.0.9    controlplane   <none>           <none>
newpods-2tv7f   1/1     Running   0          110s   10.42.0.10   controlplane   <none>           <none>
newpods-dbs6w   1/1     Running   0          110s   10.42.0.11   controlplane   <none>           <none>
newpods-7h242   1/1     Running   0          110s   10.42.0.12   controlplane   <none>           <none>
```

-----------

**How many containers are part of the pod webapp?**
```sh
$ kubectl describe pod webapp
Name:         webapp
Namespace:    default
Priority:     0
Node:         controlplane/172.25.0.84
Start Time:   Sat, 29 Jan 2022 17:36:10 +0000
Labels:       <none>
Annotations:  <none>
Status:       Pending
IP:           10.42.0.13
IPs:
  IP:  10.42.0.13
Containers:
  nginx:
    Container ID:   containerd://dd28a75bc218cec56de32b8fd23c9786251fa8d9d28c2cd6763b0685fa7918f7
    Image:          nginx
    Image ID:       docker.io/library/nginx@sha256:2834dc507516af02784808c5f48b7cbe38b8ed5d0f4837f16e78d00deb7e7767
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Sat, 29 Jan 2022 17:36:12 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-l9wnn (ro)
  agentx:
    Container ID:   
    Image:          agentx
    Image ID:       
    Port:           <none>
    Host Port:      <none>
    State:          Waiting
      Reason:       ImagePullBackOff
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-l9wnn (ro)
```

-----------

**Delete the webapp Pod**
```sh
$ kubectl delete pod webapp
pod "webapp" deleted
```

-----------

**Create a new pod with the name redis and with the image redis123**
```sh
$ kubectl run redis --image=redis123 --dry-run=client -o yaml
```
```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: redis
  name: redis
spec:
  containers:
  - image: redis123
    name: redis
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```