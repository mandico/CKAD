Readiness and Liveness Probes
- HTTP Test - /api/ready
- TCP Test - 3306
- Exec Command

```yaml
    readinessProbe:
      httpGet:
        path: /api/ready
        port: 8080
      tcpSocket:
        port: 3306
      exec:
        command:
          - cat
          - /app/is_ready
      initialDelaySeconds: 10
      periodSeconds: 5
      failureThreshold: 8
```
```yaml
    livenessProbe:
      httpGet:
        path: /api/ready
        port: 8080
      tcpSocket:
        port: 3306
      exec:
        command:
          - cat
          - /app/is_ready
      initialDelaySeconds: 10
      periodSeconds: 5
      failureThreshold: 8
```

Container Logging
```bash
kubectl logs [pod_name] -f
```

Monitor and Debug Applications