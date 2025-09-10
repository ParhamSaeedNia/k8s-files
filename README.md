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

- **`nginx-web-html-configmap.yml`** - HTML content for nginx index page
- **`nginx-web-deployment.yml`** - Full-featured nginx deployment with health checks, volumes, and ConfigMap
- **`nginx-web-service-nodeport.yml`** - NodePort service to expose nginx externally
- **`nginx-web-persistent-storage.yml`** - PersistentVolumeClaim for nginx content
- **`nginx-web-node-selector-deployment.yml`** - nginx deployment with nodeSelector
- **`nginx-web-node-affinity-deployment.yml`** - nginx deployment with nodeAffinity (required)
- **`nginx-web-nodename-deployment.yml`** - nginx deployment with nodeName (direct node assignment)
- **`nginx-web-specific-node-deployment.yml`** - nginx deployment with specific node assignment
- **`nginx-web-ingress.yml`** - Ingress resource for HTTP/HTTPS routing with hostname and path rules
- **`nginx-web-ingress-alternative.yml`** - Alternative Ingress configuration (renamed from parham-ingress.yml)
- **`nginx-web-service-clusterip.yml`** - ClusterIP service for Ingress backend
- **`nginx-web-service-for-ingress.yml`** - Additional ClusterIP service for Ingress
- **`nginx-web-simple-deployment.yml`** - Basic nginx deployment with minimal configuration

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

- **ConfigMaps**: `{application}-{purpose}-configmap` (e.g., `nginx-web-html-configmap`)
- **Deployments**: `{application}-{type}-deployment` (e.g., `nginx-web-simple-deployment`, `nginx-web-node-affinity-deployment`)
- **Services**: `{application}-service-{type}` (e.g., `nginx-web-service-nodeport`, `nginx-web-service-clusterip`)
- **Storage**: `{application}-{type}-storage` (e.g., `nginx-web-persistent-storage`)
- **Ingress**: `{application}-ingress` or `{application}-ingress-{variant}` (e.g., `nginx-web-ingress-alternative`)
- **Containers**: `{application}-container` (e.g., `nginx-web-container`)
- **App Labels**: `{application}-{purpose}` (e.g., `nginx-web-simple`, `nginx-web-node-affinity`)

## 🔗 Resource Relationships

Each application folder contains all related resources that work together:

- ConfigMaps are referenced by their corresponding Deployments
- Services select Pods using matching labels
- Deployments reference PVCs for persistent storage
- All names are consistent across related resources

## ✨ Recent Improvements

**Naming Standardization (Latest Update):**

- Removed personal names (e.g., `parham-ingress.yml` → `nginx-web-ingress-alternative.yml`)
- Standardized all container names to `nginx-web-container`
- Improved service naming to distinguish types (`nginx-web-service-nodeport`, `nginx-web-service-clusterip`)
- Enhanced deployment names with descriptive suffixes (`nginx-web-simple-deployment`, `nginx-web-node-affinity-deployment`)
- Updated all cross-references between resources to maintain consistency
- Made all app labels follow the pattern `nginx-web-{purpose}` for better organization
