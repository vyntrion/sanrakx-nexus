# Testing and Quality Plan

## Backend

Use pytest and FastAPI's test client where appropriate.

Test: - Health endpoint - Valid and invalid event schemas - JSON and CSV
upload limits - Timestamp parsing and timezone normalization - Detection
thresholds and time windows - Alert evidence references - Database
persistence and duplicate handling - Status transition validation -
Intelligence collector timeouts and malformed responses - Report
generation - Authorization and rate limiting once implemented

## Frontend

Use Vitest and a React testing library if selected.

Test: - Loading, empty, and error states - Search, filters, and
pagination - Alert detail and status updates - API failures - Accessible
labels and keyboard navigation - Responsive layout

## End-to-end acceptance scenario

1.  Start backend and frontend.
2.  Load a known synthetic dataset.
3.  Run detection.
4.  Confirm a known rule triggers.
5.  Open the alert and verify its evidence.
6.  Add a note and update status.
7.  Export a report.
8.  Restart backend and verify persistence.
9.  Simulate an external feed failure and confirm cached records remain.
10. Confirm no secret or raw stack trace appears in user-facing errors.

## Definition of done

A feature is done when code, tests, documentation, and a reproducible
demo exist. Record test results and unresolved limitations. Do not claim
coverage or detection performance without measurement.
