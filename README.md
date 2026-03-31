# sowmiya-architecture-diagram

## Simple Architecture for Cost-effective

```
                         Internet
                             |
                    Route53 (DNS)
                  (*.yourdomain.com)
                             |
                         Public IP
                             |
                   ┌───────────────────────┐
                   │         EC2           │
                   │     (Single VM)       │
                   │                       │
                   │        NGINX          │
                   │ (Reverse Proxy + SSL) │
                   │     Let's Encrypt     │
                   │           |           │
                   │   -----------------   │
                   │   |   |   |   |   |   │
                   │  App1 App2 App3 AppN  │
                   │ (Docker Containers)   │
                   │   |   |   |   |   |   │
                   │   -----------------   │
                   │           |           │
                   │      DB Container     │
                   │   (MySQL/Postgres)    │
                   │                       │
                   │ KMS Encryption (EBS)  │
                   └───────────────────────┘
                             |
                 ---------------------------
                 |       CloudWatch        |
                 | CPU / Memory / Disk     |
                 | StatusCheckFailed       |
                 | Endpoint Monitoring     |
                 ---------------------------
                             |
                         SNS Topic
                             |
                       Email / Alert
```

## Highly Available & Scalable Architecture
