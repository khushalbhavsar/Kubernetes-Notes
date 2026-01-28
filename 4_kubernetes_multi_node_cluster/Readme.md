# How to Install a Multi-Node Kubernetes Cluster using Kind

This folder contains all the necessary files to create a multi-node Kubernetes cluster using [Kind](https://kind.sigs.k8s.io/).

Kind (Kubernetes IN Docker) is a tool for running local Kubernetes clusters using Docker container "nodes". It is primarily designed for testing Kubernetes itself, but may be used for local development or CI.

---

## Prerequisites

* **Docker** installed and running on your machine. You can download it from [here](https://www.docker.com/products/docker-desktop).
* **Kind** installed on your machine. You can follow the installation instructions from the [Kind documentation](https://kind.sigs.k8s.io/docs/user/quick-start/#installation).
* **Kubectl** installed on your machine. You can follow the installation instructions from the [Kubernetes documentation](https://kubernetes.io/docs/tasks/tools/#kubectl).

---

# 🚀 Steps to Create a Multi-Node Kubernetes Cluster using KIND

---

## Step 1: Install Prerequisites

Ensure the following are installed on your system:

* Docker
* kubectl
* KIND (Kubernetes IN Docker)

Check versions:

```bash
docker --version
kubectl version --client
kind version
```

---

## Step 2: Create a KIND Configuration File

Create a configuration file to define multiple nodes.

```bash
vi kind-multinode.yaml
```

Add the following content:

```yaml
kind: Cluster # Cluster definition
apiVersion: kind.x-k8s.io/v1alpha4 # API version
nodes: # Define cluster
- role: control-plane # Control Plane node
- role: worker # Worker node 1
- role: worker # Worker node 2
```

📌 This creates:

* 1 Control Plane node
* 2 Worker nodes

---

## Step 3: Create the Multi-Node Cluster

Use the config file to create the cluster.

```bash
kind create cluster --name multinode-cluster --config kind-multinode.yaml
```

---

## Step 4: Verify Cluster Creation

Check cluster info:

```bash
kubectl cluster-info
```

Verify nodes:

```bash
kubectl get nodes
```

Expected output:

| NAME          | STATUS |
| ------------- | ------ |
| control-plane | Ready  |
| worker        | Ready  |
| worker        | Ready  |

---

## Step 5: Check KIND Docker Containers

Verify nodes are running as Docker containers:

```bash
docker ps
```

---

## Step 6: Deploy a Test Application (Optional)

Create a sample deployment:

```bash
kubectl create deployment nginx --image=nginx
kubectl scale deployment nginx --replicas=3
```

Verify pods:

```bash
kubectl get pods -o wide
```

---

## Step 7: Expose the Application

```bash
kubectl expose deployment nginx --type=NodePort --port=80
kubectl get svc
```

---

## Step 8: Load Local Docker Image (Optional)

If using a local image:

```bash
kind load docker-image myapp:latest --name multinode-cluster
```

---

## Step 9: Delete the Multi-Node Cluster

After testing, delete the cluster:

```bash
kind delete cluster --name multinode-cluster
```

---

## 🎯 Summary

* KIND runs Kubernetes clusters inside Docker
* Multi-node clusters are created using a config file
* Ideal for local development and testing

---

## 📌 Interview One-Liner

> **KIND allows creating multi-node Kubernetes clusters locally using Docker containers defined via a configuration file.**


