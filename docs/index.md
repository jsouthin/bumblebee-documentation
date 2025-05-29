---
title: "Welcome"
owner: "joe.southin@gmail.com"
reviewers: ["joe.southin@gmail.com"]
status: approved
first_published: 2025-05-29
last_reviewed: 2025-05-29
next_review_due: 2026-05-29   # 12-month cadence
tags: [meta, entry]
---

# Welcome to Great Yellow Eng Docs

Welcome to the single source of truth for engineering procedures, design records, runbooks, and resilience plans at GY.
Everything here is treated like code—version-controlled, peer-reviewed, and published automatically via MkDocs-Material.

Powered by MkDocs - for full documentation visit [mkdocs.org](https://www.mkdocs.org).

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.


## 📂 Repository layout (top level)

| Dir | What lives here |
|-----|-----------------|
| `00_GOVERNANCE_STRATEGY/`      | Vision, OKRs, org charts, career ladders |
| `10_PROCESSES_STANDARDS/`      | SOPs, CI/CD, security policies |
| `20_ARCHITECTURE_DESIGN/`      | ADRs, HLD/LLD docs, infra diagrams |
| `30_OPERATIONAL_RESILIENCE/`   | Runbooks, DR & BCP plans |
| `40_ENABLEMENT_ONBOARDING/`    | New-hire guides, role playbooks |
| `50_KNOWLEDGE_BASE/`           | How-tos, tutorials, reference |
| `60_MEASUREMENT_REVIEW/`       | Retros, post-incident reviews, dashboards |
| `70_CROSS_FUNCTIONAL/`         | Joint guidelines with Product, IT, Security |
| `80_TOOLS_PLATFORMS/`          | Service catalog, Terraform modules |
| `90_META/`                     | Doc templates, style guides, *doc-standards* |
| `98_ARCHIVE/`                  | Immutable snapshots of retired material |

*Contributor guide → `90_META/doc-standards/00_quick-start.md`*