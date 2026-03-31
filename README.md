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
### You can refer this modern image - for simple arch diagram



<img width="1121" height="1402" alt="image" src="https://github.com/user-attachments/assets/eea80eee-fc8b-4505-b5dd-f3f8c87ad1ad" />

---
## Highly Available & Scalable Architecture

```
                           Internet
                               |
                        Route53 (DNS)
                     (*.yourdomain.com)
                               |
                        ┌─────────────┐
                        │ LoadBalancer│
                        │    (ALB)    │
                        │  ACM SSL    │
                        └─────┬───────┘
                              |
                  ┌──────────────────────────┐
                  │   Auto Scaling Group     │
                  │      (ASG)               │
                  │                          │
                  │  ┌────────────────────┐  │
                  │  │  EC2 (Primary)     │  │
                  │  │  On-Demand         │  │
                  │  │  Docker Apps       │  │
                  │  │  NGINX (optional)  │  │
                  │  └────────────────────┘  │
                  │                          │
                  │  ┌────────────────────┐  │
                  │  │  EC2 (Spot)        │  │
                  │  │  Auto-scaled       │  │
                  │  │  Docker Apps       │  │
                  │  │  NGINX (optional)  │  │
                  │  └────────────────────┘  │
                  │                          │
                  └───────────┬──────────────┘
                              |
                      ┌────────────────┐
                      │     RDS DB     │
                      │   (Multi-AZ)   │
                      └────────────────┘
                              |
                  KMS Encryption (EBS + RDS)
                              |
              -------------------------------------
              |          CloudWatch               |
              | CPU / Memory / Disk               |
              | StatusCheckFailed                 |
              | Endpoint Monitoring               |
              -------------------------------------
                              |
                          SNS Topic
                              |
                        Email / Alert

```

