# Sudo Activity Monitoring

## Overview

This detection monitors Linux log events containing sudo activity. It helps security analysts review privileged command execution and investigate activity that may require further attention.

## Detection Logic

- **Rule type:** Query
- **Index pattern:** `filebeat-*`
- **KQL query:** `message : "sudo"`
- **Execution interval:** 1 minute
- **Look-back window:** 5 minutes
- **Severity:** Medium
- **Risk score:** 50

## Testing

A controlled `sudo whoami` command was executed in the lab environment. The resulting event was collected by Filebeat, indexed in Elasticsearch, and observed in Kibana. The configured monitoring rule generated an alert during testing.

## Investigation Fields

- `@timestamp`
- `message`
- `host.name`
- `host.ip`

## Security Considerations

Sudo activity is not inherently malicious. Analysts should investigate the user, command, host, timing, and surrounding events before determining whether activity is suspicious.

## Purpose

This use case demonstrates privileged activity monitoring, query-based detection, alert validation, and security event investigation in a SIEM lab.

