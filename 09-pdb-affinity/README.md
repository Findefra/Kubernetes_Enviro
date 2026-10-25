# 09 - PodDisruptionBudget + Affinity / Anti-Affinity

**Skills demonstrated:** PodDisruptionBudget (voluntary disruptions), nodeAffinity, podAntiAffinity, topologySpreadConstraints.

## What this shows

- Protecting availability during node drains, upgrades, or cluster autoscaler scale-downs
- Spreading pods across nodes / zones for higher resilience
- Soft vs hard anti-affinity rules
- Essential for production HA workloads

## Deploy

```bash
kubectl apply -f .
kubectl get pdb,deploy,pods -l app=ha-app -o wide
```

## Cleanup

```bash
kubectl delete -f .
```
