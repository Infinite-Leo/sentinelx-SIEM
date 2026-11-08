```text
███████╗██╗███████╗███╗   ███╗
██╔════╝██║██╔════╝████╗ ████║
███████╗██║█████╗  ██╔████╔██║
╚════██║██║██╔══╝  ██║╚██╔╝██║
███████║██║███████╗██║ ╚═╝ ██║
╚══════╝╚═╝╚══════╝╚═╝     ╚═╝
```

[![SentinelX](https://img.shields.io/badge/SentinelX-SIEM%20Platform-blue?style=flat&logo=github)](https://github.com/Infinite-Leo/sentinelx-SIEM)
[![Python](https://img.shields.io/badge/Python-3.14+-3776AB?style=flat&logo=python&logoColor=white)](https://www.python.org)
[![React](https://img.shields.io/badge/React-19-61DAFB?style=flat&logo=react&logoColor=black)](https://react.dev)
[![License: AGPLv3](https://img.shields.io/badge/License-AGPL_v3-purple.svg)](https://www.gnu.org/licenses/agpl-3.0)
[![Live Demo](https://img.shields.io/badge/Live-sentinelx--xi.vercel.app-green?style=flat&logo=googlechrome)](https://sentinelx-xi.vercel.app/)
[![Docker](https://img.shields.io/badge/Docker-ready-2496ED?style=flat&logo=docker)](https://www.docker.com)

> Full-stack SIEM dashboard with real-time log correlation and MITRE ATT&CK attack scenario simulation engine.

*This is a quick overview — security theory, architecture, and full walkthroughs are in the [learn modules](#learn).*

**[Screenshots & live demo →](DEMO.md)**

## What It Does

- Real-time log ingestion and event correlation with three rule types (Threshold, Sequence, Aggregation)
- Four YAML-based attack playbooks mapped to MITRE ATT&CK (brute force, DNS tunneling, phishing, privilege escalation)
- Server-Sent Events for live alert feed with paginated, filterable log viewer
- Alert lifecycle management (acknowledge, investigate, resolve, false positive)
- Attack simulation engine that generates realistic multi-stage security events
- Built with Just for task automation with full Docker Compose deployment

## Quick Start

```bash
docker compose -f dev.compose.yml up -d
```

Visit the local development deployment at `http://127.0.0.1:8431`.

The repository also has a public deployment at [sentinelx-xi.vercel.app](https://sentinelx-xi.vercel.app/). No testing described in this repository was performed against any public deployment.

> [!TIP]
> This project uses [`just`](https://github.com/casey/just) as a command runner. Type `just` to see all available commands.
>
> Install: `curl -sSf https://just.systems/install.sh | bash -s -- --to ~/.local/bin`

## Stack

**Backend:** Flask, MongoEngine, Redis Streams, Pydantic, Argon2, JWT, Gunicorn

**Frontend:** React 19, TypeScript, Vite, TanStack Query, Zustand, visx, SCSS Modules

**Data:** MongoDB 8, Redis 7

## Learn

This project includes step-by-step learning materials covering security theory, architecture, and implementation.

| Module | Topic |
|--------|-------|
| [00 - Overview](learn/00-OVERVIEW.md) | Prerequisites and quick start |
| [01 - Concepts](learn/01-CONCEPTS.md) | Security theory and real-world breaches |
| [02 - Architecture](learn/02-ARCHITECTURE.md) | System design and data flow |
| [03 - Implementation](learn/03-IMPLEMENTATION.md) | Code walkthrough |
| [04 - Challenges](learn/04-CHALLENGES.md) | Extension ideas and exercises |

## Local Assessment Work

This repository is based on the upstream [SentinelX project](https://github.com/CarterPerez-dev/Cybersecurity-Projects/tree/main/PROJECTS/intermediate/siem-dashboard). The work below documents local security-learning and assessment activity. No production systems or third-party systems were tested.

### Documented additions

- Ran a local Brute Force with Lateral Movement simulation.
- Added the custom `Local Brute Force Login Detector` threshold rule.
- Added `docs/custom-correlation-rule.md`.
- Added `docs/incident-response-report.md`.
- Added `docs/threat-model-stride.md`.
- Added local simulation evidence under `evidence/`.
- Added local dashboard, scenario, and Log Viewer screenshots under `evidence/screenshots/`.

### Evidence boundary

The simulation was performed in a local Docker deployment at `http://127.0.0.1:8431`. The original application code and upstream learning materials were preserved as reference material.

## License

AGPL 3.0
