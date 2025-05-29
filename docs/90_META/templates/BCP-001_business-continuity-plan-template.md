---
title: "BCP-001 DC-Mall Business Continuity Plan"
owner: resilience-team@dc-mall.com
last_reviewed: 2025-05-29
next_review_due: 2025-11-29
status: approved
tags: [bcp, continuity, resilience]
---

# 1  Purpose
Ensure DC-Mall can **continue critical operations** within defined recovery time and recovery point objectives after a disruptive event.

# 2  Scope
Covers all production datacenter services, revenue-impacting SaaS platforms, and Tier 1 corporate functions (HR, Finance, Customer Support).

# 3  Definitions
| Term | Meaning |
|------|---------|
| **RTO** | Recovery Time Objective – max acceptable downtime |
| **RPO** | Recovery Point Objective – max acceptable data loss |
| **DR**  | Disaster Recovery (technical restoration) |
| **BCP** | Business Continuity Plan (people + process) |

# 4  Roles & Responsibilities
| Role | Responsibilities | Back-up |
|------|------------------|---------|
| **BCP Coordinator** (Dir. Ops) | Activate plan, liaison to execs | Senior SRE |
| **Incident Commander** | Lead response, approve comms | On-call Eng Manager |
| **Comms Lead** | External + internal updates | Product Marketing |
| **HR Lead** | Staff welfare, alt work sites | HRBP Ops |

# 5  Business Impact Summary
| Service | RTO | RPO | Impact if unmet |
|---------|-----|-----|-----------------|
| Payments API | 30 min | 5 min | Lost revenue, SLA penalties |
| Customer Portal | 4 h | 1 h | Brand damage, churn |
| Internal Email | 24 h | 4 h | Staff coordination delay |

*Full BIA lives in* `30_OPERATIONAL_RESILIENCE/dr_bcp/BIA-2025.xlsx`.

# 6  Continuity Strategies
* **Datacenter loss** → Fail-over to secondary DC within RTO via active-active A-G clusters.  
* **Key staff unavailable** → Invoke cross-training matrix (see On-Call Playbook §3).  
* **Third-party SaaS outage** → Switch to pre-configured fallback vendor; contract IDs in Vault path `kv/bcp/saas-fallbacks`.

# 7  Plan Activation
1. Incident Commander declares **BCP Level 1 / 2 / 3** based on impact table (Appendix A).  
2. Notify execs via PagerDuty Major # channel.  
3. Comms Lead approves first external statement within 45 min.

# 8  Communication Plan
| Audience | Channel | Cadence |
|----------|---------|---------|
| Employees | Slack #all-hands + email | Hourly |
| Customers | StatusPage + Twitter | 1 h, then 4 h |
| Regulators | Direct email templates | Within 24 h |

# 9  Recovery Procedures
## 9.1 Payments API
1. Run automated DB fail-over script:  
   ```bash
   ./scripts/failover-payments.sh --target secondary
   ```
2. Verify `/healthz` returns 200 from *secondary* cluster.  
3. Update Route 53 weight 100 % → secondary.

## 9.2 Customer Portal
<details>
<summary>Expand</summary>

*Deploy static fallback site from S3 bucket `portal-dr`.*  
...
</details>

# 10  Testing & Maintenance
| Activity | Frequency | Owner |
|----------|-----------|-------|
| Table-top simulation | Quarterly | BCP Coordinator |
| Full fail-over drill | Yearly | SRE Lead |
| Document review | 6 months | Section owners |

Automated reminder triggered by `next_review_due` front-matter.

# 11  References
* DR Runbook `RUN-015_datacenter-failover.md`  
* PIR template `60_MEASUREMENT_REVIEW/pir_template.md`  
* ISO 22301 control mapping `security-compliance/mappings.csv`

---

*Last tested:* 2025-03-17   *Test report:* `30_OPERATIONAL_RESILIENCE/dr_bcp/tests/BCP_test_2025-03-17.pdf`
