# Kubernetes AI Troubleshooting Agent

A simple web app that helps you troubleshoot Kubernetes clusters. It scans your namespace, finds problems, collects evidence, and explains likely root causes using AI.

---

## The problem

When something breaks in Kubernetes, you usually:

- Switch between clusters and namespaces
- Run many `kubectl` commands
- Read pod events, deployment status, and service endpoints
- Piece together what went wrong and why

That takes time and is easy to get wrong under pressure.

---

## How this app helps

This app connects to your existing cluster access (your local `kubeconfig`) and guides you through troubleshooting in a few clicks:

1. **Health scan** — Checks pods, deployments, services, ingress, and events in a namespace.
2. **Issue detection** — Highlights anomalies (e.g. failing pods, unavailable deployments).
3. **Investigation** — Collects relevant cluster data for the issue you pick.
4. **AI root cause analysis** — Sends that evidence to OpenRouter and returns a clear explanation and suggested next steps.

It does not change your cluster. It only reads information you already have access to.

---

## How it works (basic flow)

1. **Select a cluster** — From the contexts in your kubeconfig.
2. **Select a namespace** — The area you want to check.
3. **Run a health scan** — See overall status and any issues.
4. **Pick an issue** — Investigation and AI analysis run for that problem.
5. **Review the results** — Root cause summary plus the collected evidence.

Open the UI at **http://localhost:8080** and follow the steps on screen.

---

## Prerequisites

Before you start, make sure you have:

| Requirement | Why |
|-------------|-----|
| **Docker Desktop** | Runs the app |
| **kubectl** and a working **kubeconfig** (`~/.kube/config`) | Cluster access |
| **OpenRouter API key** | AI root cause analysis |
| **Cluster already reachable** | e.g. minikube running, or EKS configured on your machine |

**Minikube:** Start minikube on your machine before using the app.

**Amazon EKS:** Log in on your host first (e.g. `aws sso login`) and ensure your kubeconfig points to the cluster. The app uses the same credentials from your machine.

---

## Quick start

From the `publish` folder in this repository:

### 1. Configure the API key

```bash
cd publish
cp backend/.env.example backend/.env
```

Edit `backend/.env` and set your OpenRouter key:

```env
OPENROUTER_API_KEY=your_api_key_here
```

### 2. Start the app

```bash
docker compose up -d
```

### 3. Open the UI

Go to **http://localhost:8080**

### 4. Stop the app

```bash
docker compose down
```

To stop and remove persisted investigation history:

```bash
docker compose down -v
```

---

## URLs

| Service | URL |
|---------|-----|
| Web UI | http://localhost:8080 |
| API | http://localhost:8001 |
| API docs | http://localhost:8001/docs |
