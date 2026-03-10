# Deployment Guide

## Overview

Rosetta is Dockerized and infrastructure-agnostic. It can be deployed locally for development and testing, or to any cloud or on-premise environment that supports Docker containers.

---

## Requirements

| Requirement | Minimum |
|---|---|
| Docker Desktop | Latest stable version |
| RAM | 8GB minimum |
| Operating System | Ubuntu (WSL recommended on Windows), macOS, Linux |
| Python | 3.10+ (if running outside Docker) |
| Port | 8000 (default, configurable) |

---

## Local Deployment

### Step 1 — Clone the Repository

```bash
git clone https://github.com/Trivian-Technologies/syzygy-rosetta-originbase.git
cd syzygy-rosetta-originbase
```

### Step 2 — Build the Docker Image

```bash
docker build -t rosetta .
```

### Step 3 — Run the Container

```bash
docker run -p 8000:8000 rosetta
```

### Step 4 — Verify the Deployment

Navigate to the Swagger UI to confirm the API is running:

```
http://localhost:8000/docs
```

Or test the endpoint directly:

```bash
curl -X POST http://localhost:8000/evaluate \
  -H "Content-Type: application/json" \
  -d '{
    "input": "Test prompt",
    "context": {
      "environment": "staging",
      "industry": "general"
    }
  }'
```

You should receive a structured JSON response with `decision`, `risk_score`, `confidence`, and `timestamp`.

---

## Running Without Docker

If you prefer to run Rosetta directly without Docker:

### Step 1 — Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 2 — Start the Server

```bash
uvicorn app:app --host 0.0.0.0 --port 8000
```

### Step 3 — Test the Endpoint

```bash
curl -X POST http://localhost:8000/evaluate \
  -H "Content-Type: application/json" \
  -d '{"input": "Test prompt"}'
```

---

## Environment Configuration

Environment variables can be used to configure Rosetta's behavior:

| Variable | Default | Description |
|---|---|---|
| `PORT` | `8000` | Port the API runs on |
| `LOG_PATH` | `logs/evaluations.json` | Path for evaluation logs |
| `ENV` | `staging` | Deployment environment |
| `DEFAULT_INDUSTRY` | `general` | Default industry context |

Set these in a `.env` file at the project root or pass them directly to Docker:

```bash
docker run -p 8000:8000 \
  -e ENV=production \
  -e DEFAULT_INDUSTRY=healthcare \
  rosetta
```

---

## Production Deployment Considerations

When deploying Rosetta to a production environment:

**Reverse Proxy**
Place Rosetta behind a reverse proxy (Nginx, Traefik) to handle TLS termination, rate limiting, and load balancing.

**Persistent Log Storage**
Mount a volume for log persistence so evaluation logs survive container restarts:

```bash
docker run -p 8000:8000 \
  -v /your/host/logs:/app/logs \
  rosetta
```

**Network Security**
Do not expose port 8000 directly to the public internet. Route all traffic through your reverse proxy and restrict direct container access to internal networks only.

**Resource Limits**
Set Docker resource limits appropriate to your expected evaluation volume:

```bash
docker run -p 8000:8000 \
  --memory="2g" \
  --cpus="1.0" \
  rosetta
```

---

## Dockerfile Reference

```dockerfile
FROM python:3.11
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
EXPOSE 8000
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
```

---

## Troubleshooting

**Port already in use**
```bash
# Find what is using port 8000
lsof -i :8000
# Use a different port
docker run -p 8080:8000 rosetta
```

**Container exits immediately**
```bash
# View container logs
docker logs <container-id>
```

**Dependencies not installing**
Ensure you are using Python 3.10 or higher. Check `requirements.txt` for version conflicts.

---

## Repository Structure

```
syzygy-rosetta-originbase/
├── app.py              # FastAPI application + /evaluate endpoint
├── main.py             # Core evaluate logic
├── reflex.py           # Rosetta reflex engine
├── risk_scoring.py     # ML risk scoring module
├── safety_layer.py     # Safety tagging pre-classifier
├── requirements.txt    # Python dependencies
├── Dockerfile          # Container configuration
└── logs/
    └── evaluations.json  # Evaluation log storage
```

---

## Next Steps

- [Read the API documentation →](api-docs.md)
- [Explore the architecture →](architecture.md)
- [View the roadmap →](roadmap.md)
- [Contributing to Rosetta →](contributing.md)
