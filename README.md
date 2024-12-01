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
cosmocloud-deploy/
├── Chart.yaml           # Metadata about the chart
├── values.yaml          # Default configuration values
├── templates/           # Kubernetes manifests
│   ├── backend-deployment.yaml
│   ├── frontend-deployment.yaml
│   ├── redis-deployment.yaml
│   ├── backend-service.yaml
│   ├── frontend-service.yaml
│   ├── redis-service.yaml
│   ├── ingress.yaml    
│   └── serviceaccount.yaml
└── README.md          

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
## Instructions to Deploy and Test
Prerequisites
A Kubernetes cluster (Minikube, Kind, or cloud provider).
kubectl CLI installed and configured.
Helm CLI installed (version 3.x or later).
Deployment Steps
Clone the Repository:

git clone https://github.com/GarimaSaini2/cosmocloud-deploy.git
cd cosmocloud-deploy

## Install the Chart: Deploy the application using Helm:
Set Up Your Environment:

Ensure that a Kubernetes cluster is running. This can be achieved using tools like Minikube (for local testing) or a cloud provider like AWS, GCP, or Azure.
Install and configure the following tools:
kubectl: To manage the Kubernetes cluster.
Helm: To deploy and manage the Cosmocloud Helm chart.
Clone the Repository:

Start by cloning the repository containing the Cosmocloud Helm chart to your local system:
git clone https://github.com/GarimaSaini2/cosmocloud-deploy.git
cd cosmocloud-deploy
Deploy the Helm Chart:

Use the following Helm command to install the Cosmocloud stack:
1. Install the Helm chart:
helm install cosmocloud ./cosmocloud-deploy --atomic --timeout 60s
Explanation:
cosmocloud: The name of the Helm release.
./cosmocloud-deploy: The path to the Helm chart directory.
--atomic: Ensures the deployment is rolled back automatically if any step fails.
--timeout 60s: Sets a 60-second timeout for the deployment.

2.Verify the deployment:
   Check Pods: kubectl get pods
   Check Services: kubectl get services
   
3.Access the frontend service:   If using Minikube: minikube service frontend-svc

## Troubleshooting Common Issues
1. Pods Stuck in Pending or CrashLoopBackOff
Reason: Insufficient resources or image pull errors.
Solution:
Check pod logs for details:
kubectl logs <pod-name>
Verify container image availability.
2. Services Not Accessible
Reason: Incorrect service type or port configuration.
Solution:
Check the service configuration:
kubectl describe svc <service-name>
Ensure the correct port and service type (NodePort or ClusterIP) are set.
3. Backend or Frontend Connection Issues
Reason: Incorrect environment variables or misconfigured service names.
Solution:
Check environment variables in backend-deployment.yaml and frontend-deployment.yaml.
Verify service names and ensure they match across deployments.
4. Redis Connectivity Problems
Reason: Misconfigured Redis service or REDIS_URI in backend.
Solution:
Verify the Redis service is running:
kubectl get pods -l app=redis
Ensure the REDIS_URI environment variable is correctly set.
Customization
You can customize the deployment by modifying values.yaml or using Helm’s --set flag.
Examples
Change backend replicas:
helm install cosmocloud ./cosmocloud-deploy --set backend.replicaCount=3
Use a custom Redis image:
redis:
  image: custom-redis-image:latest
