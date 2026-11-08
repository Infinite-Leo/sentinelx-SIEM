# Threat Model (STRIDE) - SentinelX Deployment

## 1. System overview

Local Docker deployment:

Browser
→ Nginx reverse proxy on `127.0.0.1:8431`
→ React/Vite frontend
→ Flask API
→ MongoDB and Redis Streams

The backend exposes JWT-authenticated API routes. The correlation engine consumes normalized events from Redis Streams and stores events, rules, and alerts in MongoDB.

## 2. Assets

- Log and alert data
- User credentials and JWT access tokens
- Correlation rules and rule conditions
- Scenario playbooks
- MongoDB data
- Redis event streams
- API and dashboard availability

## 3. Trust boundaries

- Browser ↔ Nginx
- Nginx ↔ React frontend
- Nginx ↔ Flask API
- Flask API ↔ MongoDB
- Flask API and correlation engine ↔ Redis Streams
- Scenario playback ↔ event ingestion and correlation engine

## 4. STRIDE analysis

| Component | Threat | Example threat | Existing control | Recommended control |
| --- | --- | --- | --- | --- |
| Authentication API | Spoofing | Attacker guesses or steals credentials | JWT authentication and password hashing are implemented in the backend | Use strong secret management, short token lifetimes, refresh-token rotation, and HTTPS in deployment |
| API requests | Tampering | Client modifies log or rule data | Pydantic request schemas validate request structure | Enforce authorization and integrity checks on every write operation |
| Alert workflow | Repudiation | Analyst actions cannot be attributed later | Alert lifecycle states exist in the application | Store actor, timestamp, and action history for every alert-state change |
| MongoDB | Information disclosure | Database or verbose errors expose sensitive data | Database is deployed as an internal Compose service in the local setup | Use least-privilege database credentials, network restrictions, encryption, and safe error responses |
| Redis Streams | Tampering or disclosure | Unauthorized event injection or stream access | Redis is isolated on the backend Docker network | Require Redis authentication, restrict network access, and validate event producers |
| API and ingestion | Denial of service | Excessive requests consume API or stream resources | Authentication routes use rate limiting; request limits are configured | Add monitoring, queue limits, back-pressure, and deployment-level rate controls |
| Admin routes | Elevation of privilege | Normal user accesses administrative functions | Role checks are implemented on protected admin routes | Test every administrative route with a non-admin account and log denied attempts |
| Scenario runner | Tampering | Unauthorized user starts or changes simulations | Scenario endpoints require application authentication | Restrict scenario controls by role and log start, stop, pause, and resume actions |

## 5. Top 3 risks and next steps

1. Protect JWT signing secrets and enforce short-lived tokens in any non-local deployment.
2. Add auditable actor and timestamp records to alert lifecycle changes.
3. Restrict and authenticate MongoDB and Redis connections in deployed environments.

## 6. CIA mapping

- Confidentiality: Protect credentials, JWTs, logs, alerts, and database contents.
- Integrity: Validate events, rules, alert updates, and scenario controls.
- Availability: Protect the API, Redis Streams, MongoDB, and correlation engine from overload or failure.