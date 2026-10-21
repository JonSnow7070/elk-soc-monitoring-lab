# SSH Brute-Force Detection

## Overview

This detection identifies repeated failed SSH authentication attempts within a defined time window. It is intended to help identify possible brute-force activity.

## Detection Logic

- **Rule type:** Threshold
- **Index pattern:** `filebeat-*`
- **KQL query:** `message : "Failed password"`
- **Group by:** `source.ip`
- **Threshold:** 5 events
- **Look-back window:** 5 minutes
- **Execution interval:** 1 minute
- **Severity:** Medium
- **Risk score:** 50

## Testing

Controlled failed SSH login attempts were generated in the lab. The events were collected by Filebeat, indexed in Elasticsearch, and displayed in Kibana. The configured detection rule was triggered and its alert was verified.

The test used localhost, so the observed source IP was `127.0.0.1`. This was simulated lab activity, not evidence of an external attack.

## Investigation Fields

- `@timestamp`
- `message`
- `source.ip`
- `host.name`
- `host.ip`

## Purpose

This use case demonstrates basic threshold-based detection, alert validation, and investigation of SSH authentication failures.

