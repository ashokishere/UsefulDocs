## Docker vs Kubernetes

Docker and Kubernetes are both essential in containerized environments, but they serve different purposes. Here’s a detailed comparison:

### Feature Comparison

| Feature | Docker | Kubernetes |
|---------|--------|-----------|
| **Purpose** | Containerization platform | Container orchestration platform |
| **Function** | Helps create, package, and run containers | Manages, deploys, scales, and automates containerized applications |
| **Container Runtime** | Uses its own runtime (`containerd` in modern versions) | Supports multiple runtimes (`containerd`, `CRI-O`, etc.) |
| **Scaling** | Manual scaling of containers | Automatic scaling based on demand |
| **Networking** | Default bridge network (requires manual setup for multi-host networking) | Built-in networking model with service discovery |
| **Storage** | Uses volumes and bind mounts | Supports persistent storage using Persistent Volumes (PVs) and Persistent Volume Claims (PVCs) |
| **Load Balancing** | Requires third-party tools for load balancing | Built-in service discovery and load balancing through Services |
| **Self-Healing** | No built-in self-healing | Automatically restarts failed containers and reschedules workloads |
| **Configuration Management** | Uses environment variables and Docker Compose | Uses ConfigMaps and Secrets for better configuration management |
| **Complexity** | Easier to set up and use | More complex but powerful for large-scale applications |
| **Use Case** | Best for local development, single-container applications, and testing | Best for production environments with complex container orchestration needs |

---

### Examples

#### **Docker Example**

**1. Create a simple container using Docker:**
```sh
# Pull an Nginx image
docker pull nginx

# Run the container
docker run -d -p 8080:80 nginx
```

**2. Using Docker Compose for multi-container applications:**
```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "8080:80"
  db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: example
```

Run with:
```sh
docker-compose up -d
```

---

#### **Kubernetes Example**

**1. Deploy an Nginx container in Kubernetes:**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
```
Apply it with:
```sh
kubectl apply -f nginx-deployment.yaml
```

**2. Expose the deployment as a service:**
```sh
kubectl expose deployment nginx-deployment --type=LoadBalancer --port=80
```

---

### How Docker and Kubernetes Work Together
- Docker is used to **build** and **package** container images.
- Kubernetes is used to **orchestrate** and **manage** those containers at scale.

For a production-ready setup, you would typically **build a Docker image** and **deploy it using Kubernetes**.

Example workflow:
```sh
# Build a Docker image
docker build -t myapp:v1 .

# Push to a container registry
docker push myapp:v1

# Deploy in Kubernetes
kubectl run myapp --image=myapp:v1 --port=8080
