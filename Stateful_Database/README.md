# 02 - Stateful Database (PostgreSQL)

**Skills demonstrated:** StatefulSet, Headless Service, PersistentVolumeClaim templates, Init Containers, ordered pod management, stable network identities.

## Architecture

```
┌─────────────────────────────────────────────┐
│              StatefulSet: postgres          │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  │
│  │ postgres-0│  │ postgres-1│  │ postgres-2│  │
│  │  PVC-0   │  │  PVC-1   │  │  PVC-2   │  │
│  └────┬─────┘  └────┬─────┘  └────┬─────┘  │
└───────┼─────────────┼─────────────┼─────────┘
        │             │             │
        └─────────────┴─────────────┘
                      │
            Headless Service (postgres)
            DNS: postgres-0.postgres, etc.
```

## What this shows

- Stable network identity (`pod-name.service-name`)
- Stable storage (each pod gets its own PVC that survives rescheduling)
- Ordered deployment and scaling (0 → 1 → 2)
- Init container pattern for permission fixes / readiness of storage
- Suitable base for databases, message queues, or any stateful workload

> **Note:** This is a single-primary demo (replicas=1 by default). Real HA Postgres would use operators (CloudNativePG, Zalando, etc.).

## Deploy

```bash
kubectl apply -f .
kubectl get sts,pods,svc,pvc -l app=postgres
kubectl exec -it postgres-0 -- psql -U demo -d demo
```

## Cleanup

```bash
kubectl delete -f .
# PVCs are retained by default for safety – delete manually if desired
kubectl delete pvc -l app=postgres
```
