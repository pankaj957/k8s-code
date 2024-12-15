Kubernetes Ingress Configuration
This repository contains Kubernetes manifests for deploying and configuring the NGINX Ingress Controller in a Kubernetes cluster using Helm chart templates. The configuration files are designed to manage the deployment of the Ingress Controller, including the necessary roles, services, webhooks, and configurations.

Files Overview
The primary components of the ingress configuration include:

Namespace: Creates the ingress-nginx namespace where all resources related to the NGINX Ingress Controller will be deployed.
ServiceAccount: Defines a ServiceAccount used by the Ingress Controller.
ConfigMap: Configuration settings for the Ingress Controller.
RBAC Resources:
ClusterRole and ClusterRoleBinding for cluster-wide permissions required by the Ingress Controller.
Role and RoleBinding for namespace-scoped permissions.
Services: Exposes the Ingress Controller to the cluster and the outside world, including a LoadBalancer service and webhook service.
Deployment: The NGINX Ingress Controller deployment, which manages the deployment of NGINX pods.
IngressClass: Defines an IngressClass for handling the ingress resources.
Admission Webhooks: Includes validating and mutating webhooks for ingress resources to be validated by the Ingress Controller.
Jobs: A Kubernetes job for creating a secret used by the webhook server.
Key Resources
Namespace:

ingress-nginx: The namespace in which all ingress-related resources are created.
ServiceAccount:

ingress-nginx: Provides the necessary permissions to the NGINX Ingress Controller.
Deployment:

Uses the k8s.gcr.io/ingress-nginx/controller:v1.0.4 image for the Ingress Controller.
Configures the NGINX controller with necessary command arguments, including webhook, health checks, and leader election.
Service:

The ingress-nginx-controller service is exposed using an AWS Network Load Balancer (NLB) with TCP support for HTTP (80) and HTTPS (443) traffic.
IngressClass:

Defines the IngressClass resource to specify the controller used for ingress resources.
Admission Webhook:

Ensures the NGINX Ingress Controller properly handles ingress resources through a validating webhook.
Setup Instructions
Prerequisites
A running Kubernetes cluster (v1.19+).
kubectl CLI configured to access your cluster.
Optional: Helm for installation of the NGINX Ingress Controller.
Deploying the Ingress Resources
Apply the Ingress YAML Manifests: To deploy the resources defined in ingress.yaml, run the following command:

bash
Copy code
kubectl apply -f ingress.yaml
This will create the necessary resources, including the namespace, service account, RBAC roles, services, deployment, and webhook configurations.

Verify the Resources: Ensure that the resources have been deployed successfully by checking the status of the namespace, pods, and services:

bash
Copy code
kubectl get namespaces
kubectl get pods -n ingress-nginx
kubectl get services -n ingress-nginx
Testing the Ingress Controller: After deployment, you can test the Ingress Controller by creating an ingress resource in your cluster and accessing it via the load balancer's external IP.

Customization
Modify the ingress.yaml file to change configurations such as resource limits, replica count, or controller-specific arguments.
For a custom domain, update the ingress-nginx-controller service annotations and external DNS settings.
Cleanup
To remove the resources created by the Ingress controller, you can run:

bash
Copy code
kubectl delete -f ingress.yaml
Contributing
Feel free to fork this repository and open pull requests with any improvements or bug fixes.
