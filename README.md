# 🚀 AgentPulse — Cloud Deployment, DevOps & Security Isolation
**Branch:** `devops` | **Team:** `HTF26-012-AI-Developers` | **Hack the Future 26**

---

## 📖 Component Overview

The **DevOps & Cloud Subsystem** of AgentPulse handles cloud hosting automation, containerization, Infrastructure-as-Code (IaC) deployment blueprints, security sandboxing, and runtime authorization enforcement.

### Cloud Deployments & Infrastructure

1. **Render Infrastructure Blueprint** ([`render.yaml`](file:///render.yaml)):
   - Automated cloud web service configuration deploying on Render.
   - Sets up Python 3.12, dynamic port mapping, health checks (`/health`), automatic git-push redeploys, and persistent database volumes.

2. **Vercel Serverless Configuration** ([`vercel.json`](file:///vercel.json)):
   - Serverless WSGI/ASGI endpoint routing for fast edge telemetry processing.

3. **Docker Containerization** ([`Dockerfile`](file:///Dockerfile), [`docker-compose.yml`](file:///docker-compose.yml)):
   - Multi-stage slim Python container packaging both the Streamlit evaluation console and the FastAPI telemetry server in a single orchestrated stack.

### Security Hardening & Sandboxing

1. **Security Authorization Gate** ([`src/security/`](file:///src/security/)):
   - Validates required credentials before starting services to prevent accidental leaks.
   - In cloud hosting environments (Render / Vercel), auto-detects cloud hosting flags and enables safe demo mode without exposing sensitive keys.

2. **AST Static Code Inspector & Subprocess Sandbox** ([`src/sandbox/`](file:///src/sandbox/)):
   - Inspects untrusted external agent code before ingestion using Abstract Syntax Tree (AST) analysis.
   - Flags forbidden system calls (`os.system`, `subprocess.Popen`, raw socket operations, obfuscated `eval`/`exec`).
   - Runs untrusted agent steps inside isolated subprocesses with memory limits and strict execution timeouts.

3. **Security Policy** ([`SECURITY.md`](file:///SECURITY.md)):
   - Vulnerability disclosure and credential safety protocols.

---

## 🚀 Running via Docker

```bash
# Build and run container stack
docker-compose up --build
```

Access the application at `http://localhost:8501`.