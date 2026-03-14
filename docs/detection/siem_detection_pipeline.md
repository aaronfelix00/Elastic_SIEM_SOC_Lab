```
# SIEM Detection Pipeline

This document explains how raw Linux telemetry became detections in Elastic Security.

## Pipeline

```
Linux logs → Filebeat → ECS normalization → Elasticsearch → Detection rules → Alerts → Investigation
```
```
