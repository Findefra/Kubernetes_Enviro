# 10 - ResourceQuota & LimitRange

**Skills demonstrated:** Namespace resource governance, ResourceQuota, LimitRange (default + max constraints), multi-tenant isolation patterns.

## What this shows

- Preventing noisy-neighbor problems in shared clusters
- Enforcing default resource requests/limits when developers forget them
- Hard caps on total CPU, memory, and object counts per namespace
- Foundation for multi-tenant or team-based cluster usage

## Deploy

```bash
kubectl apply -f .
kubectl describe resourcequota -n team-a
kubectl describe limitrange -n team-a

# Try creating a pod that violates the limits to see enforcement
```

## Cleanup

```bash
kubectl delete -f .
# or
kubectl delete namespace team-a
```
