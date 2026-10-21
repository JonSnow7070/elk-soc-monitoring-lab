# ELK-Based SOC Monitoring Lab — Project Report

## 1. Introduction

This project implements a Security Information and Event Management (SIEM) laboratory using the Elastic Stack. The objective is to collect Linux security logs centrally, detect selected suspicious activities, generate alerts, and visualize security events through a Kibana dashboard.

## 2. Objectives

- Configure centralized log collection using Filebeat.
- Store and search collected events using Elasticsearch.
- Monitor Linux SSH authentication and sudo activity.
- Implement and test detection rules.
- Investigate security events using Kibana Discover.
- Create a dashboard for security monitoring.

## 3. Laboratory Environment

The lab consists of two Ubuntu virtual machines hosted in VirtualBox.

| Component | Configuration |
|---|---|
| ELK Server | Elasticsearch and Kibana |
| ELK Server IP | 192.168.29.135 |
| Filebeat Server IP | 192.168.29.241 |
| Elasticsearch | Version 7.17.29 |
| Kibana | Version 7.17.29 |
| Filebeat | Version 9.5.2 |

## 4. Tools and Technologies

- Ubuntu Linux
- Oracle VirtualBox
- Elasticsearch
- Kibana
- Filebeat
- Kibana Query Language (KQL)
- SSH authentication logs

## 5. Implementation

### 5.1 Log Collection

Filebeat was configured with a Filestream input to collect Linux log files and forward events to Elasticsearch using authenticated communication.

Authentication-related events from `/var/log/auth.log` were used for monitoring and testing.

### 5.2 Centralized Log Storage

Elasticsearch was configured to receive, index, and store the collected events. The indexed data was searched and analyzed through Kibana.

### 5.3 SSH Brute-Force Detection

A threshold-based detection rule was created to identify repeated failed SSH authentication attempts.

- Query: `message : "Failed password"`
- Grouping field: `source.ip`
- Threshold: 5 events
- Look-back period: 5 minutes
- Execution interval: 1 minute
- Severity: Medium
- Risk score: 50

Controlled failed SSH login attempts were generated to validate the rule. The resulting alert was observed in Kibana.

The test used localhost, so the observed source IP was `127.0.0.1`. This was a controlled simulation and not evidence of an external attack.

### 5.4 Sudo Activity Monitoring

A query-based rule was configured to monitor events containing sudo activity.

- Query: `message : "sudo"`
- Look-back period: 5 minutes
- Execution interval: 1 minute
- Severity: Medium
- Risk score: 50

The command `sudo whoami` was executed as a controlled test. The resulting event was observed in Kibana and used to validate the monitoring rule.

Sudo activity is not inherently malicious and should be assessed in context.

## 6. Alert Investigation

Kibana was used to examine collected events and generated alerts. Fields reviewed included:

- `@timestamp`
- `message`
- `source.ip`
- `host.ip`
- `host.name`

These fields help an analyst review event timing, source information, host metadata, and the underlying log message.

## 7. SOC Dashboard

A Kibana dashboard named `SOC Security Monitoring Dashboard` was created with the following visualizations:

1. Failed SSH Logins
2. Failed SSH Activity Over Time
3. SSH Activity by Host IP
4. SSH Activity by Host
5. SSH Authentication Success vs Failure
6. Sudo Activity Over Time

The dashboard provides a consolidated view of the monitored security activity.

## 8. Security Configuration

Elasticsearch authentication was enabled, Kibana authentication was configured, and Filebeat was set up to authenticate when sending events to Elasticsearch. Kibana encrypted saved objects were also configured.

Credentials and encryption keys must not be published in the repository.

## 9. Testing and Results

The following activities were validated during the lab implementation:

- Filebeat service operation.
- Ingestion of authentication events into Elasticsearch.
- Search and inspection of failed SSH authentication events in Kibana.
- Triggering of the SSH brute-force detection rule through controlled test activity.
- Observation of sudo activity and its corresponding alert.
- Creation of the SOC monitoring dashboard.

These tests demonstrate the basic end-to-end workflow of log collection, indexing, detection, alerting, and investigation in a small SIEM environment.

## 10. Challenges and Troubleshooting

During implementation, configuration and compatibility issues involving Filebeat inputs, Elasticsearch authentication, Kibana connectivity, and detection rules were investigated and resolved sufficiently to validate the monitoring workflow.

The lab provided practical experience in Linux service management, log ingestion troubleshooting, authentication configuration, and Kibana rule validation.

## 11. Conclusion

The project demonstrates a basic SOC monitoring pipeline built using the Elastic Stack. It provides practical exposure to centralized logging, Linux authentication monitoring, threshold-based detection, alert investigation, and dashboard development.

The laboratory is intended for educational use and can be extended with additional endpoints, improved detection logic, event enrichment, and notification workflows.

## 12. Future Enhancements

- Add additional Linux endpoints.
- Monitor more authentication and system security events.
- Improve detection logic and reduce false positives.
- Add network telemetry and event enrichment.
- Configure notification and incident response workflows.
- Develop additional security dashboards and detection use cases.
