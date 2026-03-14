```
# SOC Lab Architecture

This document describes the architecture of the Elastic-based SOC lab.

## Components

- Kali Linux VM: attacker machine
- Ubuntu Server VM: monitored target
- Filebeat: log shipper
- Elasticsearch: centralized log indexing
- Kibana / Elastic Security: SIEM dashboards, detections, and alerts

## Architecture Flow

```
Kali → Ubuntu → Filebeat → Elasticsearch → Kibana / Elastic Security → SOC Anture
```
```
