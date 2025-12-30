# Woodpecker CI Configuration

Self-hosted CI/CD infrastructure for our GitHub organization using [Woodpecker CI](https://woodpecker-ci.org/).

## Architecture

| Component | Location | Purpose |
|-----------|----------|---------|
| Caddy | Main server | Reverse proxy with automatic HTTPS |
| Woodpecker Server | Main server | CI/CD coordination and web UI |
| Woodpecker Agent | Any machine | Executes pipeline jobs |

## Structure
```
.
├── caddy/
│   └── Dockerfile
├── server/
│   └── Dockerfile
├── agent/
│   └── Dockerfile
├── docker-compose.yml
└── docker-compose.agent.yml
```

## Setup

### Server (Caddy + Woodpecker Server)
```bash
docker compose up -d
```

### Agent (can run on separate machines)
```bash
docker compose -f docker-compose.agent.yml up -d
```

## Configuration

Copy `.env.example` to `.env` and configure:

- `WOODPECKER_GITHUB_CLIENT` - GitHub OAuth App client ID
- `WOODPECKER_GITHUB_SECRET` - GitHub OAuth App secret
- `WOODPECKER_AGENT_SECRET` - Shared secret for agent authentication
- `WOODPECKER_HOST` - Public URL of your Woodpecker instance

## Documentation

- [Woodpecker CI Docs](https://woodpecker-ci.org/docs/intro)
- [GitHub Integration](https://woodpecker-ci.org/docs/administration/forges/github)
