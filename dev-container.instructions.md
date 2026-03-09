---
applyTo: "**/Dockerfile*,**/docker-compose.yml,**/compose.yml,**/docker-compose.yaml,**/compose.yaml,**/Makefile,**/.dockerignore,**/*.yaml,**/*.yml"
---
# Dev with Container Setup Instructions (Workspace)

## Workflow Defaults
- Assume Docker is used as the dev environment.

## Commands
- Run commands inside container using:
```bash
docker compose run --rm app <command>
```

### Ruby-related commands
- Run commands inside container with `RUBYOPT` using:
```bash
docker compose run --rm -e RUBYOPT='-W0' app <command>
```

## Testing
- Assume Docker is used for running tests.
