# Assignment 2: Dockerized Flask App with CI

A simple Flask app containerized with Docker and a GitHub Actions CI pipeline.

## Run locally

```bash
docker build -t flask-app .
docker run -d -p 5000:5000 --name flask-app flask-app
```

```bash
curl localhost:5000/health
```

**Output:**
```json
{"status":"ok"}
```

> Screenshot of curl output — see below (replace with your screenshot).

```bash
curl localhost:5000
# Hello from DevOps!
```

## Stop the container

```bash
docker stop flask-app && docker rm flask-app
```

## CI — GitHub Actions

On every push, `.github/workflows/build.yml` builds the Docker image and runs a live `/health` check against the container. No registry push required.

---

## Bug Report — Broken Dockerfile

A teammate provided this Dockerfile. Here are the three bugs and their fixes:

| # | Bug | Fix |
|---|-----|-----|
| 1 | `FORM python:3.12-slim` — `FORM` is not a valid Docker instruction | Change to `FROM python:3.12-slim` |
| 2 | `pip install -r requirement.txt` — filename is wrong | Change to `requirements.txt` (note the **s**) |
| 3 | `docker run -p 5000:8080 myapp` — app listens on port 5000 inside the container, mapping to 8080 on host means the app is unreachable at the documented port | Change to `-p 5000:5000` |
