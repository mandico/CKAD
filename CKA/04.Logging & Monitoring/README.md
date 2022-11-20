### 1. Monitor Cluster Components

Metrics Server é in-Memory

O kubelet possui um subcomponente chamado cAdvisor ou container Advisor que é responsável por recuperar as metricas de pods e expo-las para o Metrics Server.

``` bash
kubectl top nodes
kubectl top pods
```

### 2. Managing Applications Logs

``` bash
kubectl logs POD_NAME -f
kubectl logs POD_NAME CONTAINER_NAME -f
```