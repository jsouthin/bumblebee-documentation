---
title: "Naming Conventions"
owner: "joe.southin@gmail.com"
reviewers: ["joe.southin@gmail.com"]
status: approved
first_published: 2025-05-29
last_reviewed: 2025-05-29
next_review_due: 2026-05-29   # 12-month cadence
tags: [meta, template]
---

## Naming conventions

|Rule	|Example|
| ----------- | ------------------------------------ |
|kebab-case for files & dirs	|`dr-bcp/network-failover.md`|
|Semantic prefixes for repeatable artefacts	|`SOP-007_hotfix-process.md` · `ADR-0043_adopt-rust.md`|
|Date or version suffix when content changes meaningfully	|`org-chart_2025-05-01.png`|
|Templates live in `90_META/templates` so every new doc starts with the right skeleton.||

Every Markdown (or Google Doc) begins with YAML front-matter so tooling can read it:

```yaml linenums="1"
---
title: "SOP-007 Hot-fix Process"
owner: "ops-team@dc-mall.com"
reviewers: ["security@dc-mall.com"]
status: approved
first_published: 2024-11-03
last_reviewed: 2025-04-10
next_review_due: 2025-10-10   # 6-month cadence
tags: [sop, release, hotfix, production]
---
```
## Governance & upkeep

| Topic                   | Recommended practice                                                                                                                                                   |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Ownership**           | Each top-level folder has an *Area Tech Lead* as DRI; each document has a named *owner* in the front-matter.                                                           |
| **Review cadence**      | Tooling (GitHub Action / Notion reminder) checks `next_review_due` nightly and opens an issue / sends a Slack nudger.                                                  |
| **Version control**     | Use Git for markdown & diagrams (Draw\.io XML) → PR review means every change is code-reviewed and traceable.                                                          |
| **Publishing**          | Merge to `main` auto-builds and deploys a static Doc site (MkDocs-Material) *and* syncs a Notion page with backlinks.                                                  |
| **Search & tagging**    | Agree on a controlled vocabulary (`infra`, `sop`, `adr`, `product-ops`, `k8s`) stored in `90_META/taxonomy.md`. Notion databases mirror these tags for faceted search. |
| **Retire/Archive**      | Move deprecated docs to `98_ARCHIVE/<year>` using a GitHub “Archive” label; redirect links via docs-site alias.                                                        |
| **Compliance evidence** | Map SOC 2/ISO controls to document paths in a lookup table (`security-compliance/mappings.csv`) so auditors can self-serve.                                            |

## Practical tips to keep docs concise

| Principle                      | Technique                                                                                                                                 |
| ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| **Single responsibility**      | If the purpose + procedure don’t fit on ≈ 2 screens, split out child docs (“Rollback dry-run”, “Post-rollback smoke tests”).              |
| **Progressive disclosure**     | Put the *Happy Path* in main body; nest edge-case branches in collapsible `<details>` blocks (Markdown) or toggle sections (Notion/Docs). |
| **Diagrams > prose**           | A good flowchart can replace 200 words of step-if-else logic.                                                                             |
| **Link, don’t paste**          | Reference shared definitions (e.g., “production cluster”) instead of re-explaining them.                                                  |
| **Empirical length guardrail** | Lint rule: warn when a Markdown file exceeds **750 lines** or 5 embedded images; Docs/Notion: aim for ≤ 5 minute read (≈ 1,000 words).    |
| **Template section limits**    | Templates have **commented hints** like “\<Keep explanation ≤ 2 paragraphs>”. Leave them in place—CI fails if you exceed.                 |

## One-page cheatsheet (pin to your desk)
```pgsql
🧭  PREP       : search ➜ slug ➜ template
✍️  WRITE      : purpose ► procedure ► refs (≤ 750 lines)
🎨  DIAGRAMS   : .drawio + exported .png, side-by-side
✅  SELF-CHECK : make lint-docs / Doc Review checklist
🔍  REVIEW     : PR, mandatory owner + SME approvals
🚀  PUBLISH    : merge ➜ docs site ➜ Notion sync ➜ Slack ping
♻️  AFTERCARE  : update index, next_review_due = +6 mo
```

## Worked example — writing “SOP-012 Emergency Patch Roll-Back”
Below is an end-to-end checklist you can follow every time you add a document.
Actions that differ between Git/Markdown, Notion, and Google Docs are called out inline.

| Phase                    | What you do                                                                                                                                                                                                                                                                                                                                                                                                                  | Why it matters                                                                              |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| **0 — Pre-flight**       | 1. **Search first.**<br>  • In repo: `git grep -i "emergency patch rollback"`<br>  • In Notion: global search “tag\:sop AND rollback”.<br>  • In Google Drive: “type\:doc rollback SOP”.<br>2. **Check taxonomy sheet** (`90_META/taxonomy.md`) for existing tags or synonyms.                                                                                                                                               | Avoid duplicates; reuse vocabulary so search works.                                         |
| **1 — Plan**             | 3. Pick the path → `10_PROCESSES_STANDARDS/sop/`.<br>4. Pick the ID → next number in `sop-index.csv` (e.g., `012`).<br>5. Create a short **slug** → `emergency-patch-rollback`.                                                                                                                                                                                                                                              | Keeps filenames deterministic: `SOP-012_emergency-patch-rollback.md`.                       |
| **2 — Scaffold**         | 6. **Copy template** from `90_META/templates/sop_template.md` (or the matching Notion/Docs template).<br>7. Fill YAML front-matter: owner, reviewers, dates, tags: `[sop, release, rollback]`.                                                                                                                                                                                                                               | The template enforces the right sections and auto-validates in CI.                          |
| **3 — Draft content**    | 8. **Write in the rule-of-three structure**: Purpose → Procedure → References.<br>9. Keep paragraphs short (≤ 7 lines) and use ordered steps.<br>10. **Break out detail**: if a step needs > 5 sub-steps, link to a separate How-To doc instead of bloating the SOP.                                                                                                                                                         | Modular documents stay skimmable and reusable.                                              |
| **4 — Add diagrams**     | 11. Open Draw\.io → save as `SOP-012_rollback-flow.drawio` in the same folder.<br>12. **Export PNG** (400–600 px wide) for quick preview `SOP-012_rollback-flow.png`.<br>13. Embed: `![Rollback flow](SOP-012_rollback-flow.png)` (Markdown) **or** `/image` block in Notion/Docs pointing to the PNG in Drive.<br>14. If the diagram will change often, link **both** the .drawio source and the PNG so reviewers can diff. | Source files live with the doc so anyone can update them; the PNG renders on the docs site. |
| **5 — Local checks**     | 15. Markdown: run `make lint-docs` (spellcheck, linkcheck, front-matter schema).<br>   Notion / Google Docs: run through the “Doc Review” checklist (spelling, broken links).                                                                                                                                                                                                                                                | Catches easy mistakes before reviewers waste time.                                          |
| **6 — PR & review**      | 16. Commit & push: `git commit -m "docs: add SOP-012 emergency patch rollback"`.<br>17. Open PR; auto-assign reviewers listed in front-matter.<br>18. Address comments; squash-merge with “Rebase & merge”.                                                                                                                                                                                                                  | PR gives traceability; enforced review prevents tribal shortcuts.                           |
| **7 — Publish & notify** | 19. Merge triggers the docs-site CI → your SOP appears at `/10_processes_standards/sop/sop-012...` within minutes.<br>20. A GitHub Action (or Zapier) syncs the same Markdown into a Notion page.<br>21. Slack bot posts the update to **#eng-changes**.                                                                                                                                                                     | Engineers get the update where they live; no one hunts for the doc.                         |
| **8 — Aftercare**        | 22. Add link to master index (`10_PROCESSES_STANDARDS/README.md`).<br>23. Create a one-line entry in `sop-index.csv` (`012, Emergency Patch Roll-Back, 2025-05-28`).<br>24. Set `next_review_due` to +6 months. CI will remind you.                                                                                                                                                                                          | Discoverability, audit trail, and freshness all handled.                                    |

