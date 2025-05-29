---
title: "Docs-as-Code Rationale"
owner: "joe.southin@gmail.com"
reviewers: ["joe.southin@gmail.com"]
status: approved
first_published: 2025-05-29
last_reviewed: 2025-05-29
next_review_due: 2026-05-29   # 12-month cadence
tags: [meta, docs]
---

# Docs-as-Code: Why we treat docs like software

## 1  The messy reality

* Tribal knowledge in Slack threads  
* Out-of-date Google Docs nobody can find  
* Wiki “last edited 2 years ago” – yet linked from the runbook  
* Auditor asks **“Show change history for your BCP”** → 🤯

## 2  Core principles

| # | Principle | What it means in practice |
|---|-----------|---------------------------|
| 1 | **Single source of truth** | Canonical copy lives in Git `main` branch. |
| 2 | **Version control** | Every change has author, timestamp, diff. |
| 3 | **Code review** | Docs go through PR just like code. |
| 4 | **Continuous Integration** | Lint, spellcheck, schema validation on every commit. |
| 5 | **Automated publishing** | Merge → static site rebuild in < 60 s. |

## 3  Benefits for DC-Mall Engineering

* **Audit-ready** – SOC 2 & ISO 27001 love immutable history.  
* **On-call velocity** – runbooks are guaranteed current.  
* **Onboarding** – new hires clone repo, search locally; no VPN to legacy wiki.  
* **Knowledge analytics** – front-matter lets us chart stale docs, ownership gaps.  

## 4  Case studies

* **GOV.UK PaaS** moved from Confluence to GitHub → 50 % reduction in stale pages.  
* **Stripe** ADR repo surfaced 900 + architectural decisions for engineers & PMs.  

## 5  When *not* to use it

| Scenario | Better option |
|----------|---------------|
| Real-time legal redlines | Google Docs suggestions |
| Polished marketing site  | Webflow / Docusaurus public site |
| One-off whiteboard snap  | Notion page (then delete when formal doc exists) |

## 6  Next steps

* Mandatory for all **SOP, Runbook, ADR, PIR** by **2025-07-01**.  
* Other doc types migrate opportunistically.  
* Docs Guild runs monthly office-hours for questions.