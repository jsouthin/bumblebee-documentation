---
title: "DRP-001 Disaster Recovery Plan"
owner: resilience-team@dc-mall.com
last_reviewed: 2025-05-29
next_review_due: 2025-11-29
status: approved
tags: [drp, disaster-recovery, resilience]
---

# 1  Purpose
Define the **technical procedures** and recovery objectives required to
restore DC-Mall’s critical systems after a catastrophic event.

# 2  Scope
* Production workloads in **primary & secondary datacenters**  
* Supporting cloud services (AWS, GCP)  
* CI/CD infrastructure used to redeploy applications

# 3  Recovery Objectives

| Tier-1 Service | RTO | RPO |
|----------------|-----|-----|
| Payments API          | 30 min | 5 min |
| Control Plane (K8s)   | 60 min | 10 min |
| Customer Portal       | 4 h    | 1 h |

*Full RTO/RPO matrix lives in* `dr_bcp/RTO-RPO-matrix.xlsx`.

# 4  Roles & Responsibilities

| Role | Responsibilities | Backup |
|------|------------------|--------|
| **DR Coordinator** (SRE Lead) | Activate plan, track progress | Staff SRE |
| **Platform Team** | Infra rebuild, network cut-over | On-call Eng |
| **App Team Leads** | Validate app health, DB consistency | Designated senior dev |
| **Comms Lead** | StatusPage updates | Product Marketing |

# 5  Disaster Scenarios

| Scenario ID | Description | Expected action |
|-------------|-------------|-----------------|
| **DC-L1** | Full power/network loss in primary DC | Fail-over to secondary DC |
| **DB-L2** | Region-wide RDS outage | Promote cross-region read-replica |
| **K8s-L1** | Kubernetes control-plane corruption | Re-provision cluster via IaC |

# 6  Recovery Strategy (High-level)

1. **Decision to declare DR** – Incident Commander + DR Coordinator.  
2. **Switch traffic** – Global DNS & Anycast update to secondary endpoints.  
3. **Infrastructure rebuild** – Terraform apply in clean VPC.  
4. **Data restore** – Point-in-time recovery from cross-region backups.  
5. **Application validation** – Smoke tests & canary ramp-up.  
6. **Business hand-over** – Notify BCP Coordinator to resume continuity tasks.

# 7  Detailed Procedures

## 7.1  Kubernetes Control Plane Rebuild

```bash
# 1 Bootstrap new cluster
terraform workspace select dr
terraform apply -var 'cluster_version=1.29'

# 2 Join worker nodes
ansible-playbook join-workers.yml -i inventory/dr.ini
```

*Runbook:* `RUN-021_k8s-control-plane-rebuild.md`

## 7.2  Database Promotion / Point-in-Time Restore

1. Stop writes on primary (if reachable).  
2. Promote cross-region replica:

```bash
aws rds promote-read-replica \
     --db-instance-identifier prod-read-dr
```

3. Update `DB_ENDPOINT` secret in Vault path `kv/dr/db`.  
4. Run migration diff script: `scripts/db-consistency-check.sh`.

## 7.3  Global DNS Cut-over

```bash
cli53 rrset create dc-mall.com \
      --replace --ttl 30 \
      '*' A 203.0.113.10
```

Confirm propagation via `dig +trace`.  

## 7.4  Application Validation

* Grafana dashboard **DR – App Health** all green.  
* Synthetic checks `/healthz` pass for 15 min.  
* Canary user cohort < 5 % error rate.

# 8  Testing & Maintenance

| Test type | Frequency | Notes |
|-----------|-----------|-------|
| Table-top drill | Quarterly | Scenario walk-through |
| Automated fail-over (Chaos Day) | Semi-annual | 30-min live fail-over |
| Full site-switch | Annual | 8-hour exercise |

DRP review cadence tracked via `next_review_due`.

# 9  Change Management
* All infra declarations in Git; PR + code-review mandatory.  
* Significant DRP edits require **Resilience Team** + owning TL approval.

# 10  References
* BCP-001 Business Continuity Plan  
* RUN-015 Datacenter Fail-over Runbook  
* SOP-007 Hot-Fix Process  
* ISO 22301 mapping `security-compliance/mappings.csv`

---

*Last full DR test:* **2025-03-17** – success within RTO.
