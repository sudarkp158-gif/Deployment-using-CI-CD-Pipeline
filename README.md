# Deployment Using CI/CD Pipeline

A hands-on demonstration of a modern CI/CD pipeline using **GitHub Actions** and Python.

The project demonstrates how a software change can move from source control through automated validation and, as the project evolves, toward automated deployment.

## Project Objective

Build and demonstrate an end-to-end software delivery pipeline where a code change automatically moves through:

```text
Code Change
    ↓
Git Commit
    ↓
Git Push
    ↓
GitHub
    ↓
GitHub Actions
    ↓
Automated Tests
    ↓
Docker Build
    ↓
GHCR
    ↓
Render Deploy Hook
    ↓
Render
    ↓
Container Deployment
    ↓
Gunicorn
    ↓
Flask
    ↓
Health Check

```

## Technology Stack

| Area                 | Technology                       |
| -------------------- | -------------------------------- |
| Programming Language | Python                           |
| Web Framework        | Flask                            |
| Application Server   | Gunicorn                         |
| Testing              | Pytest                           |
| Containerization     | Docker                           |
| Source Control       | Git / GitHub                     |
| CI/CD                | GitHub Actions                   |
| Container Registry   | GitHub Container Registry (GHCR) |
| Cloud Deployment     | Render                           |
| Secrets              | GitHub Actions Secrets           |


## Key Program Risks and Mitigation Plan

| Risk                           | Impact                            | Mitigation                                  |
| ------------------------------ | --------------------------------- | ------------------------------------------- |
| Automated tests fail           | Deployment blocked                | Fix failing tests before deployment         |
| Docker build failure           | Release blocked                   | Validate Dockerfile and dependencies        |
| Registry push failure          | Deployment cannot proceed         | Monitor GHCR authentication and permissions |
| Deployment hook failure        | Cloud deployment not triggered    | Validate secret and deployment hook         |
| Application fails health check | Deployment may not become healthy | Validate `/health` and application runtime  |
| Dependency vulnerability       | Security exposure                 | Add dependency scanning                     |
| Bad production deployment      | Customer impact                   | Introduce rollback strategy                 |
| Configuration mismatch         | Runtime failure                   | Use environment-specific configuration      |


### Architecture Summary

                    ┌──────────────────┐
                    │     Developer    │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │     GitHub       │
                    │   Source Code    │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ GitHub Actions   │
                    │                  │
                    │ • Test           │
                    │ • Build          │
                    │ • Package        │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │       Docker     │
                    │   Build Image    │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │       GHCR       │
                    │ Container Image  │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │     Render       │
                    │ Cloud Deployment │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │    Gunicorn      │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │      Flask       │
                    │   Application    │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │  /health =       │
                    │    healthy       │
                    └──────────────────┘
