---
title: "Quick Start"
owner: "joe.southin@gmail.com"
reviewers: ["joe.southin@gmail.com"]
status: approved
first_published: 2025-05-29
last_reviewed: 2025-05-29
next_review_due: 2026-05-29   # 12-month cadence
tags: [meta, docs, quick-start]
---

# 🚀 Quick-Start

Welcome! If you need to write **any** engineering doc – SOP, runbook, ADR, or just a how-to –
follow the **five-minute path** below.

We use [MkDocs-Materials](https://squidfunk.github.io/mkdocs-material/) for the framework/delivery, GitHub for the repository, and YAML Front-Matter as standard.  


| Step | What you do | Command / Click |
|------|-------------|-----------------|
| 1 | **Pull latest** docs repo | `git pull origin main` |
| 2 | **Choose template**<br>Minimal, SOP, ADR … | `docs/90_META/templates/` |
| 3 | **Copy & rename** | `cp template_sop.md 10_PROCESSES_STANDARDS/sop/SOP-###_<slug>.md` |
| 4 | **Fill YAML** header | `title`, `owner`, dates, tags |
| 5 | **Write content**<br>(≤ 750 lines!) | VS Code / Notion |
| 6 | **Preview** locally | `mkdocs serve` |
| 7 | **Commit & PR** | `git commit -m "docs: add SOP-042..."` |
| 8 | **Merge → publish** | CI builds site + posts in **#eng-changes** |

## Read next
* [01 Docs-as-Code Rationale](01_docs-as-code-rationale.md) — why we do this.  
* [02 MkDocs Overview](02_mkdocs-overview.md) — how the toolchain works.  
* [05 Example (Minimal)](05_example-doc-minimal.md) — copy-paste starter.

