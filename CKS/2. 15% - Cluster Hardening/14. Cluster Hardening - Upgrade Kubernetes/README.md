Kubernetes Release Cycles

major.minor.patch
1.19.2

- Minor version every 3 months
- No LTS (Long Term Support)

---

How to upgrade a cluster
- First upgrade the master components
    - apiserver, controller-manager, scheduler

- Then the worker components
    - kubelet, kube-proxy

- Components same minor version as apiserver
    - or one below

---

How to upgrade a node

1. kubectl drain
    - Safely evict all pods from node.
    - Mark node as SchedulingDisabled (kubectl cordon)

2. Do the upgrade

3. kubectl uncordon
    - Unmark node as ShedulingDisabled

---

How to make your application survive an upgrade
- Pod gracePeriod / Terminating state
- Pod Lifecycle Events
- PodDisruptionBudget