# 06 - Kustomize Overlays (Base + Environments)

**Skills demonstrated:** Kustomize, base + overlays pattern, environment-specific customization without duplicating manifests, image tags, replica counts, ConfigMap generators.

## Structure

```
06-kustomize-overlays/
├── base/                  # Shared resources
│   ├── deployment.yaml
│   ├── service.yaml
│   └── kustomization.yaml
└── overlays/
    ├── dev/               # Dev: 1 replica, debug image, lower resources
    │   └── kustomization.yaml
    └── prod/              # Prod: 3 replicas, production image, higher resources
        └── kustomization.yaml
```

## What this shows

- DRY principle applied to Kubernetes manifests
- Environment promotion workflow (dev → prod)
- Common Kustomize transformers: namePrefix, images, replicas, patches
- Ready for GitOps (Argo CD / Flux can point at overlays)

## Usage

```bash
# Preview
kubectl kustomize overlays/dev
kubectl kustomize overlays/prod

# Apply
kubectl apply -k overlays/dev
kubectl apply -k overlays/prod
```

## Cleanup

```bash
kubectl delete -k overlays/dev
kubectl delete -k overlays/prod
```
