# 🗳️ Microservices Voting App on Azure Kubernetes Service (AKS)

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Azure](https://img.shields.io/badge/Microsoft_Azure-0089D0?style=for-the-badge&logo=microsoft-azure&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![YAML](https://img.shields.io/badge/YAML-000000?style=for-the-badge&logo=yaml&logoColor=white)

## 📋 Project Overview

A comprehensive DevOps project demonstrating the deployment of a microservices-based voting application on Azure Kubernetes Service (AKS). This project showcases advanced container orchestration, cloud infrastructure management, and complete Kubernetes manifest development.

### 🎯 Key Achievements

- ✅ Created and configured an AKS cluster on Azure
- ✅ Developed complete Kubernetes manifest files for each microservice
- ✅ Implemented deployments, services, pods, and replica sets
- ✅ Deployed a multi-tier application architecture
- ✅ Demonstrated container orchestration best practices

## 🏗️ Architecture Overview

This voting application follows a microservices architecture pattern with the following components:

### 🔧 Application Components

| Component      | Technology   | Purpose                   | Port |
| -------------- | ------------ | ------------------------- | ---- |
| **Voting App** | Python/Flask | Frontend voting interface | 80   |
| **Result App** | Node.js      | Results display interface | 80   |
| **Worker**     | .NET Core    | Vote processing service   | -    |
| **Redis**      | Redis        | In-memory cache/queue     | 6379 |
| **PostgreSQL** | PostgreSQL   | Persistent database       | 5432 |

## 📸 Project Screenshots

### 🖼️ Deployment Process

![AKS Cluster Setup](voting/Capture%20d'écran%202025-04-14%20142305.png)
_AKS cluster creation and configuration_

![Kubernetes Deployment](voting/Capture%20d'écran%202025-04-15%20115719.png)
_Kubernetes manifest deployment process_

### 🌐 Application Interface

![Voting Interface](voting/Capture%20d'écran%202025-04-19%20004315.png)
_Voting application frontend interface_

![Results Display](voting/Capture%20d'écran%202025-04-19%20004326.png)
_Real-time results display_

### ⚙️ Cluster Management

![Pod Management](voting/Capture%20d'écran%202025-04-19%20004340.png)
_Kubernetes pod management and monitoring_

![Service Configuration](voting/Capture%20d'écran%202025-04-19%20235104.png)
_Service discovery and load balancing_

### 📊 Monitoring & Scaling

![Application Scaling](voting/Capture%20d'écran%202025-04-20%20002855.png)
_Horizontal pod autoscaling demonstration_

![Cluster Monitoring](voting/Capture%20d'écran%202025-04-20%20005335.png)
_Azure Monitor integration and metrics_

![Production Deployment](voting/Capture%20d'écran%202025-04-20%20005350.png)
_Final production deployment on AKS_



### 📊 Application Flow

```
[Voting App] → [Redis] → [Worker] → [PostgreSQL] → [Result App]
```

1. Users cast votes through the **Voting App**
2. Votes are queued in **Redis**
3. **Worker** processes votes from Redis
4. Processed votes are stored in **PostgreSQL**
5. **Result App** displays real-time results

## 🛠️ Technology Stack

### ☁️ Cloud & Infrastructure

- **Microsoft Azure** - Cloud platform
- **Azure Kubernetes Service (AKS)** - Managed Kubernetes
- **Azure CLI** - Command-line management

### 🐳 Container Orchestration

- **Kubernetes** - Container orchestration platform
- **kubectl** - Kubernetes command-line tool
- **Docker** - Containerization platform

### 📋 Configuration Management

- **YAML Manifests** - Kubernetes configuration files
- **Container Registry** - Image storage and management

## 🚀 Deployment Instructions

### Prerequisites

- Azure CLI installed and configured
- kubectl installed
- Active Azure subscription
- Docker (for local testing)

### 1. Create AKS Cluster

```bash
# Create resource group
az group create --name voting-app-rg --location eastus

# Create AKS cluster
az aks create \
  --resource-group voting-app-rg \
  --name voting-app-cluster \
  --node-count 3 \
  --enable-addons monitoring \
  --generate-ssh-keys

# Get credentials
az aks get-credentials --resource-group voting-app-rg --name voting-app-cluster
```

### 2. Deploy Application Components

```bash
# Deploy all components in order
kubectl create -f voting-app-deploy.yaml
kubectl create -f voting-app-service.yaml
kubectl create -f redis-deploy.yaml
kubectl create -f redis-service.yaml
kubectl create -f postgres-deploy.yaml
kubectl create -f postgres-service.yaml
kubectl create -f result-app-deploy.yaml
kubectl create -f result-app-service.yaml
kubectl create -f worker-app-deploy.yaml
```

### 3. Verify Deployment

```bash
# Check all pods
kubectl get pods

# Check all services
kubectl get services

# Check deployments
kubectl get deployments
```

### 4. Access Applications

```bash
# Get external IPs
kubectl get services

# Or use port forwarding for testing
kubectl port-forward service/voting-service 8080:80
kubectl port-forward service/result-service 8081:80
```

### 5. Scale Applications

```bash
# Scale voting app for high availability
kubectl scale deployment voting-app-deploy --replicas=3

# Scale result app
kubectl scale deployment result-app-deploy --replicas=2
```

## 🔧 Configuration Details

### Service Types

- **NodePort Services**: For external access during development
- **ClusterIP Services**: For internal service communication
- **LoadBalancer**: For production external access

### Resource Management

- **CPU/Memory Limits**: Configured for optimal resource utilization
- **Replica Sets**: Ensuring high availability
- **Health Checks**: Liveness and readiness probes

### Security Features

- **Network Policies**: Controlling pod-to-pod communication
- **RBAC**: Role-based access control
- **Secrets Management**: Secure credential handling

### ☁️ Cloud-Native Patterns

- **Microservices Architecture**: Loosely coupled service design
- **Stateless Applications**: Scalable frontend services
- **Persistent Storage**: StatefulSets for database components
- **Configuration Management**: ConfigMaps and Secrets

## 📈 Monitoring & Observability

### 📊 Azure Monitor Integration

- **Container Insights**: Pod and node-level monitoring
- **Application Performance**: Real-time performance metrics
- **Log Analytics**: Centralized logging and analysis
- **Alerting**: Proactive issue detection

### 🔍 Kubectl Commands for Monitoring

```bash
# View pod logs
kubectl logs -f deployment/voting-app-deploy

# Check pod resource usage
kubectl top pods

# Monitor events
kubectl get events --sort-by=.metadata.creationTimestamp
```

## 🚀 Future Enhancements

### 🔄 CI/CD Pipeline

- **Azure DevOps**: Automated build and deployment pipelines
- **GitOps**: Git-based deployment workflows
- **Container Registry**: Automated image building and scanning

### 🛡️ Security Improvements

- **Pod Security Policies**: Enhanced security constraints
- **Network Segmentation**: Advanced network policies
- **Image Scanning**: Vulnerability assessment automation

### 📊 Advanced Monitoring

- **Prometheus/Grafana**: Custom metrics and dashboards
- **Jaeger**: Distributed tracing
- **ELK Stack**: Enhanced logging and analytics

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/enhancement`)
3. Commit your changes (`git commit -am 'Add new enhancement'`)
4. Push to the branch (`git push origin feature/enhancement`)
5. Create a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Author

**Haythem532002**

- GitHub: [@Haythem532002](https://github.com/Haythem532002)

## 🙏 Acknowledgments

- Docker Samples team for the example voting app images
- Microsoft Azure team for AKS documentation
- Kubernetes community for excellent orchestration tools

---

⭐ **Star this repository if you found it helpful!** ⭐
