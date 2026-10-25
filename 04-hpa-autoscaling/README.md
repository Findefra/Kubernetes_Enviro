# 04 - Horizontal Pod Autoscaler (HPA)

**Skills demonstrated:** HorizontalPodAutoscaler, resource-based scaling, Metrics Server integration, Deployment with proper requests (required for HPA).

## Architecture

```
┌─────────────────────────────────────┐
│          HPA (CPU target 50%)       │
│  minReplicas: 2  maxReplicas: 10    │
└──────────────────┬──────────────────┘
                   │ scales
┌──────────────────▼──────────────────┐
│         Deployment: loadgen         │
│         (CPU-intensive workload)    │
└─────────────────────────────────────┘
```

## What this shows

- Declarative autoscaling based on CPU utilization
- Why resource *requests* are mandatory for HPA to function
- Scaling behavior (scale-up / scale-down policies can be tuned)
- Ready for custom metrics (Prometheus Adapter) extension

## Prerequisites

Metrics Server must be running:

```bash
# Kind / Minikube
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
# (may need --kubelet-insecure-tls patch for local clusters)
```

## Deploy & Test

```bash
kubectl apply -f .
kubectl get hpa,deploy,pods -l app=loadgen

# Generate load (in another terminal)
kubectl run -it --rm load-tester --image=busybox --restart=Never -- /bin/sh -c \
  "while true; do wget -q -O- http://loadgen; done"

# Watch scaling
kubectl get hpa -w
```

## Cleanup

```bash
kubectl delete -f .
```
