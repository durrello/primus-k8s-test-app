# primus-k8s-test-app

A Helm chart for deploying a containerised web application ("travel-website") to Kubernetes. It
packages a Deployment, Service, and Horizontal Pod Autoscaler (HPA) with configurable image,
namespace, and scaling values — a clean example of a reusable, values-driven Helm chart.

## Chart contents

```
.
├── Chart.yaml              # Chart metadata (v0.1.0, appVersion 1.16.0)
├── values.yaml             # Configurable values (image registry/tag, namespace)
└── templates/
    ├── _helpers.tpl        # Template helpers (labels, names)
    ├── deployment.yaml     # Application Deployment
    ├── service.yaml        # Service exposing the pods
    └── hpa.yaml            # HorizontalPodAutoscaler
```

## What this demonstrates

- Authoring a reusable Helm chart with templated manifests
- Values-driven configuration (image registry, tag, namespace)
- Autoscaling via an HPA template
- Helm helper templates for consistent labels and naming

## Prerequisites

- A Kubernetes cluster (kind, minikube, EKS, GKE, etc.)
- [Helm](https://helm.sh/docs/intro/install/) 3.x
- `kubectl` configured for your cluster

## Usage

```bash
# Lint the chart
helm lint .

# Render templates locally to inspect output
helm template travel-website . --namespace dev

# Install / upgrade
helm upgrade --install travel-website . \
  --namespace dev --create-namespace \
  --set global.imageTag=latest

# Uninstall
helm uninstall travel-website --namespace dev
```

## Key values

| Value | Default | Description |
|-------|---------|-------------|
| `global.imageRegistry` | `durrellgemuh` | Container image registry/namespace |
| `global.imageTag` | `latest` | Image tag to deploy |
| `global.namespace` | `dev` | Target namespace |

## License

MIT
