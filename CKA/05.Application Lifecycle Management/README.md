### 1. Rolling Updates and Rollbacks

``` bash
kubectl rollout status deployments/myapp_deployment
deployment "myapp_deployment" successfully rolled out

kubectl rollout history deployments/myapp_deployment
deployment.apps/myapp_deployment
REVISION  CHANGE-CAUSE
1         <none>
2         <none>
3         <none>

kubectl rollout undo deployments/myapp_deployment
```

Deployment Strategy
- Rolling Update (default)
- Recreate

### 2. Commands

In Dockerfile:

``` bash
CMD ["command", "PARM_1", "PARM_2"] # OK
CMD ["nginx -g daemon off;"] # NOK

CMD ["nginx", "-g", "daemon off;"]
```

### 3. Commands and Arguments

``` bash
#Dockerfile
FROM Ubuntu
ENTRYPOINT ["sleep"]
CMD ["5"]
```

``` yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: ubuntu-sleep-pod
  name: ubuntu-sleep-pod
spec:
  containers:
  - image: ubuntu-sleep-pod
    name: ubuntu-sleep-pod
    command:
      - "sleep2.0"
    args:
      - "10"
```

| Dockerfile | >>> | Manifesto |
| --- | --- | --- |
| ENTRYPOINT | >>> | command |
| CMD | >>> | args |