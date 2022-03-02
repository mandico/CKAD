Commands and Arguments
### Environment Variables
```yaml
env:
    name: APP_COLOR
    value: BLUE
```

### ConfigMaps
##### Imperative
From Literal:
```bash
kubectl create configmap my-config \
--from-literal=APP_COLOR=blue \
--from-literal=APP_MODE=prd
```
From File:
```bash
kubectl create configmap my-config \
--from-file=APP_COLOR=/tmp/app_color.txt \
--from-file=APP_MODE=/tmp/app_mode.txt
```
##### Declarative
configmap-definition.yaml
```yaml configmap-definition.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  APP_COLOR: blue
  APP_MODE: prd
```

Apply configmap file:
```bash
kubectl apply -f configmap-definition.yaml
configmap/my-config created
```

Describe configmap:
```bash
kubectl describe configmap my-config
Name:         my-config
Namespace:    default
Labels:       <none>
Annotations:  <none>

Data
====
APP_COLOR:
----
blue
APP_MODE:
----
prd

BinaryData
====

Events:  <none>
```

ConfigMap in Pod:
```yaml pod-definition-configmap.yaml
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp-color
  labels:
    name: simple-webapp-color
spec:
  containers:
  - name: simple-webapp-color
    image: mmumshad/simple-webapp-color
    ports:
      - containerPort: 8080
    envFrom:
      - configMapRef:
          name: my-config
```

Secrets
Docker Security
Security Contexts
Service Account
Resource Requirements
Tains and Tolerations
Node Selector
Node Affinity