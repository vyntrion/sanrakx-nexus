# 14-Day MVP Roadmap

## Week 1 --- Backend and detections

### Day 1 --- Repository and API skeleton

Create the repository, virtual environment, FastAPI app, health
endpoint, and initial commit.

### Day 2 --- Event schema

Define Pydantic models and normalized event fields. Add schema tests.

### Day 3 --- Synthetic data and ingestion

Create safe synthetic authentication events. Implement JSON/CSV
validation and limits.

### Day 4 --- AUTH-001

Implement repeated failed-login detection with a configurable rolling
time window.

### Day 5 --- AUTH-002 and PRIV-001

Implement failure-followed-by-success and explicit privilege-event
rules.

### Day 6 --- Test and refine

Add positive, negative, edge-case, and duplicate-event tests.

### Day 7 --- SQLite persistence

Store events, alerts, evidence references, and status updates.

## Week 2 --- Frontend and intelligence

### Day 8 --- Frontend shell

Create React/Vite pages, navigation, design tokens, and API client.

### Day 9 --- Dashboard

Connect actual counts and charts to backend responses.

### Day 10 --- Events and alerts

Add search, filters, pagination, and detail views.

### Day 11 --- Investigations

Add notes, status transitions, and evidence timelines.

### Day 12 --- Intelligence and reports

Add NVD collection, one RSS source, freshness metadata, and report
export.

### Day 13 --- Security review

Test upload handling, API errors, CORS, secrets hygiene, and collector
failures.

### Day 14 --- Portfolio release

Finish documentation, screenshots, demo recording, GitHub release, and
known-limitations section.

## Priority order if time runs short

1.  Working detection engine and tests.
2.  Event/alert persistence.
3.  Useful dashboard connected to real backend data.
4.  One working intelligence source.
5.  Investigation notes and export.
6.  Visual polish and optional AI.

## Release acceptance criteria

-   Fresh setup is documented and reproducible.
-   Core API routes work and are tested.
-   Three documented detection rules have test cases.
-   Evidence can be traced from alert to event.
-   Intelligence records show source and timestamps.
-   No unrestricted shell execution is exposed.
-   README accurately labels implemented versus planned features.
