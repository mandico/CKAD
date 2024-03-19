Immuntability

Container and Pod Level Enforcement

- Remove bash and shell
- Make filesystem read-only
    - SecurityContexts and PodSecurityPolicies
- Run as user and non root

Scenarios to ensure Pod`s containers are immutable


```bash
kubectl run immutable --image=httpd -o yaml --dry-run=client > pod_v0.yaml
kubectl create -f pod_v0.yaml
kubectl exec -it immutable -- bash

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

```bash
kubectl delete -f pod_v0.yaml --force --grace-period 0

kubectl -f pod_v1.yaml create

kubectl exec -it immutable -- bash
root@immutable:/usr/local/apache2# touch test
bash: touch: command not found
```

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

```bash
kubectl delete -f pod_v1.yaml --force --grace-period 0

kubectl -f pod_v2.yaml create

kubectl exec -it immutable -- bash
OCI runtime exec failed: exec failed: unable to start container process: exec: "bash": executable file not found in $PATH: unknown
command terminated with exit code 126
```

```
kubectl delete -f pod_v2.yaml --force --grace-period 0
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

```bash
kubectl -f pod_v3.yaml create

kubectl exec -it immutable -- bash

root@immutable:/usr/local/apache2# touch /tmp/test
touch: cannot touch '/tmp/test': Read-only file system
root@immutable:/usr/local/apache2# touch /usr/local/apache2/logs/test
root@immutable:/usr/local/apache2# ls -ltrh /usr/local/apache2/logs/
total 4.0K
-rw-r--r-- 1 root root 2 Mar 19 19:56 httpd.pid
-rw-r--r-- 1 root root 0 Mar 19 19:57 test
```