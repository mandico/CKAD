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

A security context defines privilege and access control settings for a Pod or Container. Security context settings include, but are not limited to:

Discretionary Access Control: Permission to access an object, like a file, is based on user ID (UID) and group ID (GID).

Security Enhanced Linux (SELinux): Objects are assigned security labels.

Running as privileged or unprivileged.

Linux Capabilities: Give a process some privileges, but not all the privileges of the root user.

AppArmor: Use program profiles to restrict the capabilities of individual programs.

Seccomp: Filter a process's system calls.

-----------------
Service Account
Resource Requirements
Tains and Tolerations


Node Selector
``` bash
kubectl labels node <node-name> <label-key>:<label-value>
kubectl labels node mynode size:Large
```

pod-definition-selector.yaml
``` yaml
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp-color
  labels:
    name: simple-webapp-color
spec:
  containers:
  - name: simple-webapp-color
    image: nginx
  nodeSelector:
    size: Large
```


Node Affinity