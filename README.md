1. The Purpose of the Chart
Provide an explanation of what the Helm chart does, such as deploying a complete application stack consisting of a backend, frontend, and Redis.
# Cosmocloud Deploy Helm Chart

This Helm chart deploys a complete application stack for Cosmocloud consisting of:
- Backend (Node.js API)
- Frontend (React.js)
- Redis Database

The chart configures each component with necessary environment variables, services, and deployments.
2. The Structure of the Chart
Explain the structure of the Helm chart and what each directory/file contains.
## Chart Structure

- `Chart.yaml`: Contains metadata about the chart (name, version, description, etc.).
- `values.yaml`: Contains default configuration values for the backend, frontend, and Redis services.
- `templates/`: Contains the Kubernetes manifests for deployment, service, etc.
  - `backend-deployment.yaml`: Kubernetes deployment for the backend.
  - `frontend-deployment.yaml`: Kubernetes deployment for the frontend.
  - `redis-deployment.yaml`: Kubernetes deployment for Redis.
  - `service.yaml`: Kubernetes service definitions for all components.
- `README.md`: This file, containing instructions and details about the Helm chart.
3. Instructions to Deploy and Test It
Provide instructions for deploying the Helm chart and testing it.
## Instructions to Deploy

1. Install the Helm chart:
   ```bash
   helm install cosmocloud-deploy ./cosmocloud-deploy --atomic --timeout 30s
2.Verify the deployment:

   Check Pods: kubectl get pods
   Check Services: kubectl get services
3.Access the frontend service:

   If using Minikube: minikube service frontend-svc
## Common Issues
Issue: Pods are stuck in CrashLoopBackOff
Check the pod logs:
kubectl logs <pod-name>
Check if the container image is correct and accessible.
Issue: Frontend service is not accessible
Ensure the frontend service type is set to NodePort and the correct port is exposed.
If using Minikube, use minikube service frontend-svc to access the service.
