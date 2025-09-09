# Kubernetes Course Files - Organized by Application

This directory contains Kubernetes manifests organized by application groups for better learning and understanding.

## 📁 Directory Structure

### 🗄️ `manifests/mysql-database/`

Complete MySQL database application with all related resources:

- **`mysql-configmap.yml`** - Environment variables for MySQL (MYSQL_ROOT_PASSWORD)
- **`mysql-database-deployment.yml`** - Main MySQL deployment with persistent storage
- **`mysql-database-storage.yml`** - PersistentVolumeClaim for MySQL data
- **`mysql-alternative-configmap.yml`** - Alternative ConfigMap with different key name
- **`mysql-alternative-deployment.yml`** - Alternative deployment using specific ConfigMap key reference

### 🌐 `manifests/nginx-web-server/`

Complete nginx web server application with various deployment patterns:

- **`nginx-configmap.yml`** - HTML content for nginx index page
- **`nginx-web-deployment.yml`** - Full-featured nginx deployment with health checks, volumes, and ConfigMap
- **`nginx-web-service.yml`** - NodePort service to expose nginx
- **`nginx-web-storage.yml`** - PersistentVolumeClaim for nginx content
- **`nginx-node-selector-deployment.yml`** - nginx deployment with nodeSelector
- **`nginx-node-affinity-deployment.yml`** - nginx deployment with nodeAffinity (required)
- **`nginx-specific-node-deployment.yml`** - nginx deployment with nodeName (direct node assignment)
- **`nginx-web-ingress.yml`** - Ingress resource for HTTP/HTTPS routing with hostname and path rules
- **`nginx-web-service-for-ingress.yml`** - ClusterIP service for Ingress backend
- **`simple-nginx-deployment.yml`** - Basic nginx deployment with 3 replicas

### 🔧 `manifests/standalone-pods/`

Individual Pod examples and their services:

- **`basic-nginx-pod.yml`** - Simple nginx Pod with labels
- **`test-nginx-pod.yml`** - Test nginx Pod
- **`standalone-nginx-service.yml`** - Service for standalone nginx pods

## 🎯 Key Learning Concepts

### ConfigMaps

- Environment variable injection (`envFrom`)
- Specific key references (`configMapKeyRef`)
- Configuration data storage

### Deployments

- Replica management
- Pod templates and selectors
- Health checks (liveness/readiness probes)
- Volume mounting
- Node scheduling (selectors, affinity)

### Services

- Pod selection via labels
- Port mapping
- Service types (NodePort)

### Storage

- PersistentVolumeClaims
- Volume mounting in containers
- Data persistence

### Pod Scheduling

- **nodeSelector**: Hard requirement for specific node labels
- **nodeAffinity**: Advanced scheduling rules (required/preferred)
- **nodeName**: Direct node assignment (bypasses scheduler)

### Ingress

- HTTP/HTTPS routing with hostname rules
- Path-based routing with different path types
- Service backend configuration
- Ingress controller integration

## 🚀 How to Use

1. **Deploy a complete application:**

   ```bash
   kubectl apply -f manifests/mysql-database/
   kubectl apply -f manifests/nginx-web-server/
   ```

2. **Deploy individual resources:**

   ```bash
   kubectl apply -f manifests/standalone-pods/basic-nginx-pod.yml
   ```

3. **Check resource status:**
   ```bash
   kubectl get pods,services,configmaps,pvc
   ```

## 📝 Naming Convention

All resources now use descriptive, consistent naming:

- **ConfigMaps**: `{application}-config` or `{application}-{type}-config`
- **Deployments**: `{application}-deployment` or `{application}-{type}-deployment`
- **Services**: `{application}-service` or `{application}-{type}-service`
- **Storage**: `{application}-storage` or `{application}-{type}-storage`
- **Containers**: `{application}-container`

## 🔗 Resource Relationships

Each application folder contains all related resources that work together:

- ConfigMaps are referenced by their corresponding Deployments
- Services select Pods using matching labels
- Deployments reference PVCs for persistent storage
- All names are consistent across related resources
