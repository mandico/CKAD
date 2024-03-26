NetworkPolicies
- Firewall Rules in Kubernetes
- Implemented by the Network Plugins CNI (Calico  / Weave)
- Namespace Level

By default every pod can access every pod
Pod are **not** isolated

Multiple NetworkPolicies:
- Possible to have multiples NPs selecting the same pods.
- If a pod has more than one NP:
    - then the union of all NPs applied.
    - order doesn`t affect policy result.

#### Default Deny

```bash
kubectl run frontend --image=nginx 
kubectl run backend  --image=nginx

kubectl expose pod frontend --port 80
kubectl expose pod backend  --port 80

kubectl exec frontend -- curl backend
kubectl exec backend  -- curl frontend
```

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: default-deny
  namespace: default
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  - Egress
```

``` bash
kubectl -f default-deny.yaml create
```

#### Allow frontend pods to talk to backend pods
allow_frontend_to_backend.yaml
default-deny-allow-dns.yaml

#### Allow backend pods to talk to database pods
allow_frontend_to_backend_to_database.yaml

Scenarios