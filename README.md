# GY Engineering Knowledge Base

Welcome to the **single source of truth** for engineering procedures, design records, runbooks, and resilience plans at GY.  
Everything here is treated *like code*—version-controlled, peer-reviewed, and published automatically via MkDocs-Material.

---

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

---

## 🔧 Quick start for contributors

```bash
# 1 . Clone & install docs tooling
git clone git@github.com:jsouthin/bumblebee-documentation.git
cd bumblebee-documentation
pip install mkdocs-material

# 2 . Serve the site locally (hot-reload)
mkdocs serve
```

Then open <http://localhost:8000> in your browser.

---

## 📑 Writing a new document

1. **Pick a template** in `docs/90_META/templates/` (SOP, Runbook, ADR …).  
2. **Copy & rename** — e.g. `SOP-042_hotfix-process.md`.  
3. Fill YAML front-matter (`title`, `owner`, dates, tags).  
4. Write content (≤ 750 lines) and open a PR.  
5. Merge → CI builds & deploys; **#eng-changes** posts a summary.

Details in `90_META/doc-standards/`.

---

## 🖼️ Diagrams

Commit the editable `.drawio` **alongside** a rendered `.svg` or `.png`.  
A pre-commit hook regenerates the image so source and render stay in sync.

---

## 🛡️ License

Documentation © 2025 DC-Mall Engineering.  
Released under the MIT License unless a file header states otherwise.
