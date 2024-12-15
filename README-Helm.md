# Ingress NGINX Helm Chart

This Helm chart deploys the [Ingress NGINX Controller](https://kubernetes.github.io/ingress-nginx/) on a Kubernetes cluster. The controller acts as a reverse proxy, load balancer, and ingress controller for Kubernetes applications.

## Features
- NGINX as the ingress controller for managing ingress resources
- Supports TLS termination and SSL passthrough
- Configurable with various ingress options
- Webhook support for validating ingress configurations

## Prerequisites
- Kubernetes 1.16 or higher
- Helm 3.x
- kubectl

## Installation

### 1. Add the Ingress NGINX repository

First, add the Ingress NGINX Helm chart repository:

```bash
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
2. Install the Chart
To install the Ingress NGINX Controller, use the following Helm command:

bash
Copy code
helm install ingress-nginx ingress-nginx/ingress-nginx --namespace ingress-nginx --create-namespace
This will install the Ingress NGINX controller in the ingress-nginx namespace. If you want to customize the chart configuration, you can create a values.yaml file with your customizations and apply it during installation:

bash
Copy code
helm install ingress-nginx ingress-nginx/ingress-nginx --namespace ingress-nginx --create-namespace -f values.yaml
3. Verify Installation
Check if the ingress controller is running by using:

bash
Copy code
kubectl get pods -n ingress-nginx
You should see a pod named ingress-nginx-controller running in the ingress-nginx namespace.

Configuration
The Helm chart is highly configurable via the values.yaml file. You can specify different parameters to customize the deployment:

Controller replicas: Set the number of replicas for the ingress controller.
Service type: Set the service type to ClusterIP, LoadBalancer, or NodePort for different ingress access.
TLS support: Configure TLS termination for secure connections.
You can check all configurable values by running:

bash
Copy code
helm show values ingress-nginx/ingress-nginx
Uninstall
To uninstall the Ingress NGINX controller, run the following command:

bash
Copy code
helm uninstall ingress-nginx --namespace ingress-nginx
This will remove the deployment, but not the namespace or persistent resources like secrets or ConfigMaps.

Troubleshooting
Ingress resources not routing: Ensure the ingress resources are correctly defined and linked to the right service.

No external IP: If using LoadBalancer type service, make sure your cloud provider supports this type and properly provisioned external IPs.

Pod issues: Inspect the ingress controller logs for any issues using:

bash
Copy code
kubectl logs -n ingress-nginx <ingress-nginx-controller-pod>
License
This Helm chart is distributed under the Apache 2.0 License.

markdown
Copy code

### Explanation:
- **Installation steps**: Guide to add the repository and install the chart.
- **Customization**: Allows users to adjust configuration using the `values.yaml` file.
- **Uninstallation**: How to uninstall the chart and its components.
- **Troubleshooting**: Common issues and their solutions.
- **License**: Specifies the license for the Helm chart.

If you need to include specific details for your Helm chart or have any additional custom configurations, feel free to modify it further.
