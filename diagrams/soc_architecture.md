```
                  ATTACKER ENVIRONMENT
                ┌───────────────────────┐
                │       Kali Linux       │
                │  Hydra / Nmap / SSH    │
                └───────────┬───────────┘
                            │
                            │ SSH attack traffic
                            ▼

                    TARGET ENVIRONMENT
                ┌───────────────────────┐
                │      Ubuntu Server     │
                │       SSH Service      │
                │      auth.log file     │
                └───────────┬───────────┘
                            │
                            │ Log collection
                            ▼

                     LOG SHIPPER LAYER
                ┌───────────────────────┐
                │        Filebeat        │
                │  Sends logs to SIEM    │
                └───────────┬───────────┘
                            │
                            │ Event ingestion
                            ▼

                      SIEM PLATFORM
                ┌───────────────────────┐
                │     Elasticsearch      │
                │   Security log store   │
                └───────────┬───────────┘
                            │
                            │ Visualization & detection
                            ▼

                ┌───────────────────────┐
                │        Kibana          │
                │  Elastic Security SIEM │
                │ Dashboards & Alerts    │
                └───────────┬───────────┘
                            │
                            │ Investigation
                            ▼

                       SOC OPERATIONS
                ┌───────────────────────┐
                │      SOC Analyst       │
                │ Detection & Response   │
                └───────────────────────┘ 
```
