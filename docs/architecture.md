# Architecture

## 1. Purpose

This document describes the intended components and boundaries of
SanrakX Nexus. It is a design contract; implementation may evolve as the
MVP is built.

## 2. Components

-   **Frontend:** React/Vite pages for dashboard, events, alerts,
    intelligence, investigations, and reports.
-   **API:** FastAPI routes validate requests, enforce authorization,
    and call application services.
-   **Event service:** Parses and normalizes supported input formats.
-   **Detection engine:** Runs deterministic rules against normalized
    events.
-   **Intelligence collectors:** Pull public data from configured APIs
    and feeds with timeouts and retry limits.
-   **Database:** SQLite for local MVP persistence.
-   **Report service:** Produces a report from stored alert evidence and
    investigation notes.
-   **Restricted operations service:** Exposes named, allowlisted
    diagnostic operations only.
-   **Optional AI adapter:** Summarizes selected evidence; never
    replaces deterministic detection.

## 3. Data flow

1.  A user uploads a supported log file or the collector retrieves
    external records.
2.  Input is validated and normalized.
3.  Normalized events or intelligence records are deduplicated and
    persisted.
4.  Detection rules evaluate eligible events.
5.  Alerts retain rule identifiers and references to supporting events.
6.  The frontend retrieves records through the API.
7.  Analysts add notes, update status, and export reports.

## 4. Trust boundaries

-   Browser to API: untrusted client input; validate every request.
-   API to database: use parameterized queries and controlled
    transactions.
-   Collector to external source: external response is untrusted and may
    be malformed.
-   AI provider/model: output is untrusted and must be labelled as
    generated.
-   Local command integration: high-risk boundary; do not expose
    arbitrary commands over HTTP.

## 5. Deployment modes

### Local MVP

Single user, local backend, SQLite, synthetic datasets, no public shell
access.

### Later multi-user deployment

Requires authentication, authorization, secure secret management, HTTPS,
database migrations, backups, rate limiting, audit logs, and operational
monitoring. Consider PostgreSQL if concurrency or multi-user
requirements exceed SQLite's intended use.

## 6. Reliability principles

-   External-source failures must not erase cached records.
-   Store fetched-at and source publication timestamps separately.
-   Make collector runs idempotent where possible.
-   Set network timeouts and bounded retries.
-   Return clear error states without exposing secrets or stack traces.
-   Use UTC internally and convert for display.
