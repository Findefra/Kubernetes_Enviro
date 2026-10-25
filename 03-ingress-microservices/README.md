# 03 - Ingress & Microservices Routing

**Skills demonstrated:** Multi-Deployment architecture, path-based Ingress routing, TLS secret (self-signed for demo), Service discovery between services.

## Architecture

```
                   ┌──────────────────┐
                   │  Ingress         │
                   │  /api  → backend │
                   │  /     → frontend│
                   └────────┬─────────┘
                            │
          ┌─────────────────┴─────────────────┐
          │                                   │
┌─────────▼────────┐               ┌──────────▼─────────┐
│ frontend         │               │ backend            │
│ Deployment + Svc │               │ Deployment + Svc   │
│ (nginx)          │               │ (simple http echo) │
└──────────────────┘               └────────────────────┘
```

## What this shows

- Clean separation of frontend and backend services
- Ingress as the single entry point (L7 routing)
- Path-based traffic splitting
- TLS termination at the Ingress (certificate secret)
- Ready for canary / blue-green extensions via Ingress annotations

## Prerequisites

- An Ingress Controller must be installed (nginx-ingress, traefik, AWS Load Balancer Controller, etc.)
- For local testing: `minikube addons enable ingress` or `kind` with ingress

## Deploy

```bash
kubectl apply -f .
kubectl get ingress,svc,deploy -l project=microservices
# After Ingress gets an address:
curl -k https://<ingress-ip>/
curl -k https://<ingress-ip>/api
```

## Cleanup

```bash
kubectl delete -f .
```
