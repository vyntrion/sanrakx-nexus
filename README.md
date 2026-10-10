# SanrakX Nexus

### Unified Cybersecurity Intelligence & Operations Workspace

**One workspace. Complete security intelligence.**

SanrakX Nexus is a defensive cybersecurity portfolio project that brings
security-event analysis, explainable detections, threat-intelligence
collection, incident investigations, and reporting into one modular
workspace.

> **Status:** Documentation and MVP blueprint\
> **Primary users:** SOC analysts, blue-team learners, and security
> researchers\
> **Initial deployment:** Local development environment\
> **Project goal:** Demonstrate practical Python, API, data, testing,
> and secure-development skills.

## Contents

-   [Project goals](#project-goals)
-   [MVP features](#mvp-features)
-   [Architecture](docs/architecture.md)
-   [API contract](docs/api.md)
-   [Detection rules](docs/detections.md)
-   [Security model](docs/security.md)
-   [Threat intelligence](docs/threat-intelligence.md)
-   [Installation](docs/setup.md)
-   [Testing](docs/testing.md)
-   [Roadmap](docs/roadmap.md)
-   [Contributing](CONTRIBUTING.md)

## Project goals

1.  Ingest supported synthetic or authorized security logs.
2.  Normalize events into a common schema.
3.  run explainable, deterministic detection rules.
4.  Preserve alert evidence and analyst decisions.
5.  Collect public vulnerability and security-news metadata.
6.  Provide traceable source links, timestamps, and synchronization
    status.
7.  Demonstrate secure API and application design.

## MVP features

-   React + Vite frontend.
-   Python + FastAPI backend.
-   SQLite persistence for a local MVP.
-   JSON/CSV event import with strict validation.
-   Rule-based alert generation and evidence references.
-   Alert search, filtering, notes, and status changes.
-   NVD vulnerability collector and one RSS news collector.
-   Incident report export.
-   Automated tests and clear documentation.

## Planned architecture

``` mermaid
flowchart TD
    Analyst --> Web[React + Vite UI]
    Web <--> API[FastAPI REST API]
    API --> Detection[Detection Engine]
    API <--> DB[(SQLite)]
    Collector[Scheduled Collectors] --> NVD[NVD API]
    Collector --> RSS[Approved RSS Feeds]
    Collector --> DB
    API --> Reports[Report Service]
    API --> Console[Restricted Local Operations]
    API -. optional .-> AI[AI Assistant]
```

## Technology choices

  Area              Initial choice          Reason
  ----------------- ----------------------- -------------------------------------------
  UI                React + Vite            Fast local development
  Styling           Tailwind CSS            Consistent responsive UI
  Charts            Recharts                Dashboard visualizations
  API               FastAPI + Pydantic      Typed request validation and OpenAPI docs
  Storage           SQLite                  Low-friction local MVP
  HTTP              Requests                External feed/API collection
  RSS               Feedparser              RSS/Atom parsing
  Tests             pytest; Vitest for UI   Regression coverage
  Version control   Git                     Auditable development history

## Quick start

See [docs/setup.md](docs/setup.md). The short version: 1. Install Python
3.11+, Node.js LTS, npm, and Git. 2. Create a Python virtual environment
in `backend/`. 3. Install dependencies from `backend/requirements.txt`.
4. Run the FastAPI service. 5. Install and run the frontend. 6.
Configure the frontend API base URL and CORS allowlist.

## Safety boundaries

-   Use synthetic logs or data from systems you are authorized to
    monitor.
-   Do not expose arbitrary shell execution through a web endpoint.
-   Do not commit API keys, secrets, private logs, or databases
    containing sensitive data.
-   Treat external articles, logs, and AI output as untrusted data.
-   Do not represent an alert as proof of compromise without
    corroborating evidence.

## Project status

This repository blueprint describes intended behavior. A feature should
be labelled **implemented** only after its code, tests, and
documentation exist. Do not claim production readiness until
authentication, authorization, deployment hardening, backups, and
operational monitoring have been reviewed.

## License

Select a license before publishing. If choosing MIT, include the
complete MIT license text in `LICENSE`.
