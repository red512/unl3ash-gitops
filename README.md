# unl3ash-gitops

GitOps manifests for the [unl3ash](https://github.com/red512/unl3ash) project.

> Full project documentation is in the [application repo README](https://github.com/red512/unl3ash).

## Related Repositories

- **[unl3ash](https://github.com/red512/unl3ash)** — Application source code, CI/CD pipelines, Dockerfile
- **[unl3ash-gitops](https://github.com/red512/unl3ash-gitops)** — Helm chart, ArgoCD application manifests
- **[unl3ash-terraform](https://github.com/red512/unl3ash-terraform)** — Infrastructure as Code (EKS, VPC, IAM, S3, ECR)

## Overview

ArgoCD watches this repo and auto-syncs the Helm chart to EKS with **auto-sync**, **self-heal**, and **prune** enabled.

- **Deployment** — Non-root container, read-only filesystem, all capabilities dropped
- **Service** — LoadBalancer (AWS ALB), port 80 -> 3000
- **HPA** — CPU-based autoscaling, 1-3 replicas at 80% threshold
- **ServiceAccount** — Annotated with IRSA role ARN for S3 access

## Project Structure

```
unl3ash-gitops/
├── argocd/
│   └── apps/
│       ├── unl3ash-app.yaml          # ArgoCD Application for unl3ash
│       └── metrics-server-app.yaml   # ArgoCD Application for metrics-server
└── helm/
    └── unl3ash-helm-chart/
        ├── Chart.yaml
        ├── values.yaml
        └── templates/
            ├── deployment.yaml
            ├── service.yaml
            ├── hpa.yaml
            └── serviceaccount.yaml
```
