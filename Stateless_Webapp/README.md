# 01 - Stateless Web Application

**Skills demonstrated:** Deployment, ClusterIP Service, ConfigMap, Resource Requests/Limits, Liveness & Readiness Probes, RollingUpdate strategy.

## Architecture

```
┌─────────────────┐
│   ConfigMap     │ ──► Environment variables / HTML content
└────────┬────────┘
         │
┌────────▼────────┐     ┌──────────────┐
│   Deployment    │────►│  ClusterIP   │
│  (3 replicas)   │     │   Service    │
│  nginx:1.25     │     │  port 80     │
└─────────────────┘     └──────────────┘
```

## What this shows

- Declarative desired state with Deployment
- Zero-downtime rolling updates (`maxUnavailable: 0`, `maxSurge: 1`)
- Proper resource management (requests + limits)
- Health probes so Kubernetes only routes traffic to healthy pods
- ConfigMap for non-sensitive configuration (12-factor style)

## Deploy

```bash
kubectl apply -f .
kubectl get all -l app=webapp
kubectl port-forward svc/webapp 8080:80
# Open http://localhost:8080
```

## Cleanup

```bash
kubectl delete -f .
```
