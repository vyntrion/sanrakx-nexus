# Security Requirements and Threat Model

## Assets

-   Imported security events and logs
-   Alert evidence and analyst notes
-   API keys and configuration secrets
-   Local database and generated reports
-   External-source credentials, if used

## Threats

-   Malformed or oversized uploads
-   SQL injection
-   Cross-origin requests from untrusted sites
-   Unauthorized alert modification
-   Abuse of manual refresh endpoints
-   Malicious content embedded in logs or external reports
-   Prompt injection against an optional AI assistant
-   Secret leakage through Git, logs, or frontend bundles
-   Remote command execution through a terminal feature
-   Denial of service through excessive requests or expensive parsing

## Required controls

### Input handling

-   Validate schemas, field lengths, timestamps, and enum values.
-   Enforce file-size and record-count limits.
-   Never execute uploaded files.
-   Treat all external content as untrusted.
-   Use parameterized SQL.

### API access

-   Restrict CORS to known frontend origins.
-   Add authentication and authorization before multi-user/public
    deployment.
-   Rate-limit sensitive and expensive endpoints.
-   Use timeouts for outbound HTTP requests.
-   Return sanitized error responses.
-   Apply pagination and bounded query ranges.

### Secrets

-   Keep API keys server-side.
-   Use environment configuration or a secret manager.
-   Exclude `.env`, databases, logs, and local environments from Git.
-   Rotate any secret that is accidentally published.

### Terminal safety

-   Never pass user-controlled text directly to a shell.
-   Expose only predefined operations in the MVP.
-   Do not provide public unauthenticated shell access.
-   A future desktop agent needs explicit consent, least privilege, an
    allowlist, execution limits, and audit logs.

### AI safety

-   Label generated summaries.
-   Keep evidence separate from model interpretation.
-   Do not follow instructions embedded in retrieved documents.
-   Do not send private logs to external services without authorization.
-   Require human review for consequential actions.

## Release checklist

-   [ ] No secrets committed.
-   [ ] Upload limits and validation tested.
-   [ ] SQL uses parameters.
-   [ ] CORS allowlist is explicit.
-   [ ] State-changing endpoints have access controls appropriate to
    deployment.
-   [ ] External requests have timeouts and bounded retries.
-   [ ] Terminal is restricted to named operations.
-   [ ] Dependencies reviewed.
-   [ ] Backup and retention policy documented.
-   [ ] Known limitations published.
