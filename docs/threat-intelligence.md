# Threat Intelligence Collection

## Purpose

Collect public vulnerability and security-news metadata into a
searchable, source-attributed view. This is not a guarantee of complete
coverage or real-time delivery.

## Initial sources

### NIST National Vulnerability Database

Official API documentation:
https://nvd.nist.gov/developers/vulnerabilities

Collect CVE identifiers, descriptions, published/modified timestamps,
available severity metrics, and source references. Respect rate limits
and use the API key only on the backend if configured.

### CISA

-   Advisories:
    https://www.cisa.gov/news-events/cybersecurity-advisories
-   Known Exploited Vulnerabilities:
    https://www.cisa.gov/known-exploited-vulnerabilities-catalog

Use official access methods and preserve original links. Treat inclusion
in a catalog as a prioritization signal, not proof of exposure in the
user's environment.

### CERT-In

Official website: https://www.cert-in.org.in/

Verify current public access methods, publication terms, and any feed
availability before implementing automated collection.

### RSS

Use feeds from reputable publishers that explicitly provide them.
Respect feed terms and avoid republishing full copyrighted articles.
Store metadata, short excerpts when permitted, and links to original
sources.

## Normalized intelligence record

Suggested fields: - `source_name` - `source_record_id` - `record_type`
(`news`, `advisory`, `vulnerability`) - `title` - `description` -
`published_at` - `modified_at` - `source_url` - `cve_ids` - `severity`
and `severity_source`, when supplied - `fetched_at` - `content_hash` for
deduplication

## Collector behavior

1.  Request with a timeout.
2.  Validate response status and shape.
3.  Parse records into the normalized schema.
4.  Normalize timestamps to UTC.
5.  Deduplicate using source identity and stable IDs.
6.  Store records transactionally.
7.  Record last attempt, last success, and error category.
8.  Keep previously stored data if the source fails.

## Scheduling

For the MVP, provide a manual refresh and a simple scheduled job with
bounded frequency. Avoid creating a new scheduler per web request.
Ensure only one collector run for a source executes at a time.

## Freshness and confidence

Show the original publication time and last fetched time separately.
Label the source and link clearly. Do not present a feed item as a
verified incident without corroboration.
