Immuntability

Container and Pod Level Enforcement

- Remove bash and shell
- Make filesystem read-only
    - SecurityContexts and PodSecurityPolicies
- Run as user and non root

Scenarios to ensure Pod`s containers are immutable


Create manifest simple pod:
```bash
kubectl run immutable --image=httpd -o yaml --dry-run=client > pod_v0.yaml
```
```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: immutable
  name: immutable
spec:
  containers:
  - image: httpd
    name: immutable
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```
Create pod and execute *bash* and *touch*:
```bash
$ kubectl -f pod_v0.yaml create
pod/immutable created

$ kubectl exec -it immutable -- bash
root@immutable:/usr/local/apache2# touch /test
root@immutable:/usr/local/apache2# bash 
root@immutable:/usr/local/apache2# 
```
Delete pod:
```bash
$ kubectl delete -f pod_v0.yaml --force --grace-period 0
pod "immutable" force deleted
```

Clone *pod_v0.yaml* and increment *startupProbe*:
```bash
cp -Rvf pod_v0.yaml pod_v1.yaml
```

```yaml
...
    startupProbe:
      exec:
        command:
        - rm
        - /bin/touch
...
```
Create pod and try execute *touch*:
```bash
$ kubectl -f pod_v1.yaml create
pod/immutable created

$ kubectl exec -it immutable -- bash
root@immutable:/usr/local/apache2# touch /test
bash: touch: command not found
```
Delete pod:
```bash
$ kubectl delete -f pod_v1.yaml --force --grace-period 0
pod "immutable" force deleted
```
Clone *pod_v0.yaml* and increament *startupProbe*:
```
cp -Rvf pod_v0.yaml pod_v2.yaml
```

```yaml
...
    startupProbe:
      exec:
        command:
        - rm
        - /bin/bash
...
```
Create pod and try execute *bash*:
```bash
$ kubectl -f pod_v2.yaml create
pod/immutable created

$ kubectl exec -it immutable -- bash
OCI runtime exec failed: exec failed: unable to start container process: exec: "bash": executable file not found in $PATH: unknown
command terminated with exit code 126
```
Delete pod:
```
$ kubectl delete -f pod_v2.yaml --force --grace-period 0
pod "immutable" force deleted
```

Clone *pod_v0.yaml* and increament *securityContext* to *readOnlyRootFilesystem*:
```
cp -Rvf pod_v0.yaml pod_v3.yaml
```
```yaml
...
    securityContext:
      readOnlyRootFilesystem: true
    volumeMounts:
    - mountPath: /usr/local/apache2/logs/
      name: cache-volume
  volumes:
  - name: cache-volume
    emptyDir:
      sizeLimit: 500Mi
...
```
Create pod and try execute *touch /test*:
```bash
$ kubectl -f pod_v3.yaml create
pod/immutable created

$ kubectl exec -it immutable -- bash
root@immutable:/usr/local/apache2# touch /test
touch: cannot touch '/test': Read-only file system
```