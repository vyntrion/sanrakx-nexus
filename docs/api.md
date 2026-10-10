# API Contract

**Base path:** `/api/v1`\
**Format:** JSON unless an endpoint explicitly returns a file.\
**Status:** Planned contract; implement routes and schemas before
marking them available.

## Conventions

-   Use ISO 8601 timestamps in UTC.
-   Paginate collection endpoints.
-   Validate enum values and request sizes.
-   Return standard HTTP status codes.
-   Require authorization for state-changing operations in any shared
    deployment.
-   Never expose secrets, stack traces, or raw server paths in error
    responses.

## Health and dashboard

  -----------------------------------------------------------------------
  Method                  Route                   Purpose
  ----------------------- ----------------------- -----------------------
  GET                     `/health`               Service health

  GET                     `/dashboard/stats`      Stored event/alert
                                                  counts and chart series
  -----------------------------------------------------------------------

## Events

  -----------------------------------------------------------------------
  Method                  Route                   Purpose
  ----------------------- ----------------------- -----------------------
  GET                     `/events`               List events; supports
                                                  pagination and filters

  GET                     `/events/{event_id}`    Get one event

  POST                    `/events/upload`        Upload a validated
                                                  JSON/CSV file

  POST                    `/detections/run`       Run configured rules
                                                  against eligible events
  -----------------------------------------------------------------------

Suggested query parameters: `limit`, `offset`, `from`, `to`, `host`,
`username`, `event_type`, `outcome`.

## Alerts and investigations

  Method   Route                         Purpose
  -------- ----------------------------- --------------------------------
  GET      `/alerts`                     List/filter alerts
  GET      `/alerts/{alert_id}`          Alert plus evidence references
  PATCH    `/alerts/{alert_id}/status`   Change status
  POST     `/alerts/{alert_id}/notes`    Add analyst note

Allowed status values: `open`, `investigating`, `resolved`. Define a
documented policy for reopening resolved alerts.

## Intelligence

  Method   Route                      Purpose
  -------- -------------------------- ----------------------------------------
  GET      `/intel/news`              Stored news items
  GET      `/intel/advisories`        Stored advisories
  GET      `/intel/vulnerabilities`   Stored vulnerability records
  GET      `/intel/status`            Source health and last successful sync
  POST     `/intel/refresh`           Request controlled refresh

The refresh endpoint must be authenticated or otherwise restricted,
rate-limited, and protected against repeated expensive requests.

## Reports

  Method   Route                    Purpose
  -------- ------------------------ ------------------------------------------
  POST     `/reports`               Create report for an authorized incident
  GET      `/reports/{report_id}`   Retrieve report metadata or content

## Example event

``` json
{
  "timestamp": "2026-10-10T09:15:00Z",
  "host": "lab-host-01",
  "username": "analyst-demo",
  "event_type": "login",
  "outcome": "failed",
  "source_ip": "192.0.2.10"
}
```

## Example alert

``` json
{
  "id": 1,
  "rule_id": "AUTH-001",
  "title": "Repeated failed login attempts",
  "severity": "high",
  "status": "open",
  "evidence_event_ids": [101, 102, 103],
  "created_at": "2026-10-10T09:20:00Z"
}
```

## Suggested error format

``` json
{
  "detail": {
    "code": "INVALID_EVENT",
    "message": "The uploaded event does not match the supported schema."
  }
}
```

## API acceptance criteria

-   OpenAPI docs accurately match implemented routes.
-   Uploads reject unsupported formats and oversized files.
-   Collection endpoints paginate consistently.
-   State changes validate the target status.
-   Every alert response exposes its rule ID and evidence references.
-   Tests cover successful and rejected requests.
