# 08 - Sidecar Pattern

**Skills demonstrated:** Multi-container Pods, shared volumes, sidecar for logging/metrics/proxy, init containers vs sidecars.

## Architecture

```
┌─────────────────────────────────────────┐
│                 Pod                     │
│  ┌─────────────┐    ┌─────────────────┐ │
│  │ Main App    │    │ Sidecar         │ │
│  │ (nginx)     │◄──►│ (log shipper)   │ │
│  └──────┬──────┘    └────────┬────────┘ │
│         │ shared volume      │          │
│         └──────────┬─────────┘          │
│               emptyDir                  │
└─────────────────────────────────────────┘
```

## What this shows

- Classic sidecar use-case: application writes logs → sidecar ships them
- Shared `emptyDir` volume between containers
- Independent resource limits per container
- Pattern used by Istio, Fluent Bit, Vault Agent, etc.

## Deploy

```bash
kubectl apply -f .
kubectl logs -l app=sidecar-demo -c app
kubectl logs -l app=sidecar-demo -c log-shipper
```

## Cleanup

```bash
kubectl delete -f .
```
