# Detection Engineering

## Principles

Detections must be explainable, repeatable, testable, and tied to
evidence. Severity indicates triage priority, not proof of compromise.

## Common event schema

Required fields: - `timestamp`: ISO 8601 timestamp, preferably UTC. -
`event_type`: normalized event category. - `outcome`: normalized result
where relevant. - `host`: system identifier. - `username`: account
identifier where applicable. - `source_ip`: source address where
applicable. - `event_id`: internal stable identifier. - `raw_event`:
optional original record, subject to data-minimization rules.

Reject or quarantine records that cannot be safely parsed. Do not
silently invent missing timestamps or identities.

## AUTH-001 --- Repeated failed logins

**Goal:** identify repeated authentication failures within a
configurable rolling time window.

**Logic:** filter failed login events, group by a documented key (for
example, username and source IP), sort by timestamp, and alert when the
configured threshold is reached inside the window.

**Evidence:** event IDs, first/last timestamp, count, grouping key,
threshold, and window.

**Test cases:** threshold minus one; threshold reached; events spread
outside the window; duplicate event; mixed usernames; malformed
timestamp.

## AUTH-002 --- Failed logins followed by success

**Goal:** flag a sequence that merits analyst review.

**Logic:** find a configured number of failed attempts for the same
account and relevant source, followed by a successful login inside a
defined interval.

**Evidence:** failed and successful event IDs, sequence timestamps, and
rule configuration.

**Caveat:** this pattern can be legitimate; it is not proof of account
compromise.

## PRIV-001 --- Privilege-related activity

**Goal:** identify privilege changes or administrative events requiring
review.

**MVP:** use explicit normalized event types and configurable
allowlists/conditions. Do not claim behavioral anomaly detection until a
baseline model is actually implemented and evaluated.

## Alert lifecycle

`open -> investigating -> resolved`

Each transition should record a timestamp and actor when authentication
is implemented. Notes should be append-only or otherwise auditable.

## Rule quality

For each rule, document: - Stable identifier and version - Purpose and
assumptions - Required input fields - Thresholds and time window -
Severity rationale - Evidence fields - Known false positives - Unit
tests and representative fixtures - Known blind spots

## Evaluation

Use a documented synthetic dataset with both positive and benign
examples. Report true positives, false positives, false negatives, and
test limitations where labels are available. Avoid unsupported claims
such as "detects all attacks."
