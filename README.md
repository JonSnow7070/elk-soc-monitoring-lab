# ELK-Based SOC Monitoring Lab

A hands-on Security Information and Event Management (SIEM) project built using the Elastic Stack to collect, analyze, and monitor Linux security events. This lab demonstrates centralized logging, SSH brute-force detection, sudo activity monitoring, security alerting, and SOC dashboard visualization.

## Project Objectives

- Implement centralized log collection using Filebeat.
- Store and search security events using Elasticsearch.
- Monitor Linux authentication and privileged command activity.
- Configure detection rules for repeated SSH login failures and sudo activity.
- Investigate security events and visualize monitoring results in Kibana.

## Architecture

The lab uses two Ubuntu virtual machines:

| Component | Purpose |
|---|---|
| Filebeat Server | Collects Linux logs and forwards events to Elasticsearch |
| Elasticsearch | Indexes and stores collected security events |
| Kibana | Supports log investigation, detection rules, alerts, and dashboards |

### Log Processing Workflow

```text
Linux Authentication Logs
          |
          v
       Filebeat
          |
          v
    Elasticsearch
          |
          v
        Kibana
       /      \
Detection    Dashboard
 Rules          |
       \        /
        Security
         Alerts
```

## Technologies Used

- Ubuntu Linux
- Elastic Stack: Elasticsearch 7.17.29 and Kibana 7.17.29
- Filebeat 9.5.2
- Oracle VirtualBox
- SSH authentication logs
- Kibana Query Language (KQL)

## Detection Use Cases

### 1. SSH Brute-Force Detection

A threshold-based detection rule identifies repeated failed SSH authentication attempts.

- **Query:** `message : "Failed password"`
- **Grouping field:** `source.ip`
- **Threshold:** 5 events
- **Look-back window:** 5 minutes
- **Execution interval:** 1 minute
- **Severity:** Medium

Controlled failed-login attempts were generated to test the rule and verify alert generation. The tests used localhost, so the observed source IP was `127.0.0.1`.

### 2. Sudo Activity Monitoring

A query-based rule monitors events containing sudo activity.

- **Query:** `message : "sudo"`
- **Look-back window:** 5 minutes
- **Execution interval:** 1 minute
- **Severity:** Medium

A controlled `sudo whoami` command was used to generate a test event. The event was observed in Kibana and used to validate the monitoring workflow.

Note: Sudo activity is not necessarily malicious; events require context and investigation.

## SOC Dashboard

The Kibana dashboard, `SOC Security Monitoring Dashboard`, contains visualizations for:

- Failed SSH logins
- Failed SSH activity over time
- SSH activity by host IP
- SSH activity by host
- SSH authentication success versus failure
- Sudo activity over time

## Screenshots

Evidence of the lab configuration, detection rules, alerts, and dashboard is available in the [`screenshots/`](screenshots/) directory.

## Security Configuration

- Elasticsearch authentication enabled.
- Kibana authentication configured.
- Authenticated Filebeat-to-Elasticsearch communication.
- Sensitive credentials and encryption keys excluded from example configuration files.

## Skills Demonstrated

- SIEM implementation and administration
- Linux log analysis
- Filebeat log ingestion
- Elasticsearch indexing and searching
- Kibana and KQL
- Detection rule configuration
- Security alert validation
- SSH authentication monitoring
- Privileged activity monitoring
- SOC dashboard development
- Troubleshooting and documentation

## Future Improvements

- Monitor logs from additional endpoints.
- Improve detection logic to reduce false positives.
- Add notifications and response workflows.
- Enrich events with additional network and host context.
- Expand monitoring with more security use cases.

## Disclaimer

This project is a controlled educational lab for cybersecurity learning. The authentication failures were simulated in the lab environment and do not represent a confirmed external attack.

## Dashboard Preview

![SOC Security Monitoring Dashboard](screenshots/SOC%20Dashboard-1.png)

[View all project screenshots](screenshots/)
