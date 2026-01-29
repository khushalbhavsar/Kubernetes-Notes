# Kubernetes Namespaces

## What is a Kubernetes Namespace?

A Namespace in Kubernetes is a logical isolation mechanism used to organize, separate, and manage resources within the same cluster.

Think of a namespace as a virtual cluster inside a physical cluster. It allows you to create multiple environments (like development, staging, and production) within a single Kubernetes cluster without resource conflicts.

---

## Example Kubernetes Namespace Code Snippet

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: my-namespace
```

---

## 📂 Types of Kubernetes Namespaces (Based on Usage)

### 1️⃣ Default Namespace

* Created automatically by Kubernetes
* Used when no namespace is specified

```bash
kubectl get pods   # uses default namespace
```

📌 **Not recommended for production**

---

### 2️⃣ System Namespace

Used by Kubernetes itself.

#### Examples:

* `kube-system` → core components (API server, scheduler)
* `kube-public` → publicly readable info
* `kube-node-lease` → node heartbeat info

⚠️ **Do not modify resources here**

---

### 3️⃣ Environment-Based Namespaces (Most Common)

Used to separate environments.

```text
dev   → Development
test  → Testing / QA
stage → Staging
prod  → Production
```

📌 Same app, different environments, same cluster.

---

### 4️⃣ Team-Based Namespaces

Used when multiple teams share a cluster.

```text
frontend-team
backend-team
devops-team
data-team
```

📌 Each team manages its own resources.

---

### 5️⃣ Application-Based Namespaces

Each application gets its own namespace.

```text
shop-app
payment-app
auth-app
```

📌 Useful for microservices architecture.

---

### 6️⃣ Monitoring / Logging Namespace

Used for observability tools.

```text
monitoring → Prometheus, Grafana
logging    → ELK Stack
```

📌 Isolates monitoring from application workloads.

---

### 7️⃣ Security / Admin Namespace

Used for security tools.

```text
security → Vault, OPA, Falco
```

📌 Restricted access (Ops only).

---

## 🧠 Interview-Ready Summary Table

| Namespace Type    | Purpose              |
| ----------------- | -------------------- |
| Default           | General resources    |
| System            | Kubernetes internals |
| Environment-based | Dev/Test/Prod        |
| Team-based        | Team isolation       |
| Application-based | Microservices        |
| Monitoring        | Observability        |
| Security          | Security tools       |

---

## 🧩 Real-World Kubernetes Namespace Example

### 🏢 Company Scenario

Imagine a **mid-size tech company** running **multiple applications** with **multiple teams** on **one Kubernetes cluster** to save cost and simplify management.

Instead of creating **separate clusters**, they use **Namespaces** to logically divide the cluster.

---

### 1️⃣ `dev` Namespace – Development Environment

#### 🔹 Purpose

* Used by developers for:

  * Feature development
  * Testing new code
  * Debugging

#### 🔹 Characteristics

* Frequent deployments
* Smaller CPU & memory limits
* Less strict security

#### 📌 Example

```text
dev
 ├── frontend-dev
 ├── backend-dev
 └── db-dev
```

✔ Mistakes in `dev` do **not affect production**

---

### 2️⃣ `prod` Namespace – Production Environment

#### 🔹 Purpose

* Used for **live applications**
* Accessed by **real users**

#### 🔹 Characteristics

* High availability
* Strict security (RBAC)
* Higher resources
* Minimal access (Ops team only)

#### 📌 Example

```text
prod
 ├── frontend
 ├── backend
 └── db
```

✔ Fully isolated from `dev`

---

### 3️⃣ `frontend-team` Namespace – Frontend Team

#### 🔹 Purpose

* Dedicated workspace for frontend developers
* Team manages only frontend services

#### 🔹 Benefits

* Team autonomy
* No interference from backend changes
* Independent scaling

#### 📌 Example

```text
frontend-team
 ├── ui-service
 └── static-assets
```

✔ Frontend team cannot touch backend resources

---

### 4️⃣ `backend-team` Namespace – Backend Team

#### 🔹 Purpose

* Dedicated namespace for backend developers
* Used for APIs, microservices, and databases

#### 🔹 Benefits

* Backend team controls APIs
* Secure access to databases
* Cleaner ownership

#### 📌 Example

```text
backend-team
 ├── auth-service
 ├── order-service
 └── payment-service
```

✔ Backend logic stays isolated

---

### 5️⃣ `monitoring` Namespace – Observability Tools

#### 🔹 Purpose

* Centralized monitoring & alerting
* Runs cluster-wide tools

#### 🔹 Tools

* Prometheus (metrics)
* Grafana (dashboards)

#### 📌 Example

```text
monitoring
 ├── prometheus
 └── grafana
```

✔ Monitoring continues even if app namespaces fail

---

### 6️⃣ `security` Namespace – Security & Policy Tools

#### 🔹 Purpose

* Manages security-critical components
* Restricted access

#### 🔹 Tools

* Vault (secrets management)
* OPA (policy enforcement)

#### 📌 Example

```text
security
 ├── vault
 └── opa
```

✔ Only security/DevOps teams have access

---
