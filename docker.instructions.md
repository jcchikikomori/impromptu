---
applyTo: "**/Dockerfile*,**/docker-compose.yml,**/compose.yml,**/docker-compose.yaml,**/compose.yaml,**/Makefile,**/.dockerignore"
---

# Container Setup Instructions

<!-- Docker commands inherited from common.instructions.md -->

## Dockerfile Best Practices

- Use multi-stage builds to reduce image size
- Pin base image versions (e.g., `ruby:3.2.2-slim` not `ruby:latest`)
- Order layers by change frequency (least → most)
- Combine RUN commands with `&&` to reduce layers
- Use `.dockerignore` to exclude unnecessary files
