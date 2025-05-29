---
title: "YAML Front-Matter Guide"
owner: "joe.southin@gmail.com"
reviewers: ["joe.southin@gmail.com"]
status: approved
first_published: 2025-05-29
last_reviewed: 2025-05-29
next_review_due: 2026-05-29   # 12-month cadence
tags: [meta, docs]
---

## 0 Field reference

```markdown
---
title: "SOP-007 Hot-Fix Process"
owner: ops-team@dc-mall.com
last_reviewed: 2025-05-29
next_review_due: 2025-11-29
status: approved
tags: [sop, release]
---
```

## 1  Required keys

| Field | Type   | Example                     |
|-------|--------|-----------------------------|
| title | string | *Runbook: Failover Redis*   |
| owner | email  | platform@dc-mall.com        |
| last_reviewed | date | 2025-05-29            |
| next_review_due | date | 2025-11-29          |

## 2  Optional keys
* **status** → `draft`, `approved`, `deprecated`  
* **tags** → for search facets  
* **source_doc** → Google Doc URL

## 3  Inheritance
Add a `.meta.yml` in any folder; children inherit its keys.

## 4  Validation
* `required-frontmatter` plugin → presence  
* JSON-Schema linter → types & enums

## 5  Hide nav icons
```css
.md-status--draft { --md-status: none; }
```

## 6  A field-by-field reference

| Field             | Required? | Example                             | Purpose                 |
| ----------------- | --------- | ----------------------------------- | ----------------------- |
| `title`           | ✅         | “SOP-012 Emergency Patch Roll-Back” | Nav text & search index |
| `owner`           | ✅         | `ops-team@dc-mall.com`              | Review responsibility   |
| `last_reviewed`   | ✅         | `2025-05-29`                        | CI staleness check      |
| `next_review_due` | ✅         | `2025-11-29`                        | Slack reminder          |
| `status`          | optional  | `approved` \| `draft`               | Nav badge               |
| `tags`            | optional  | `[sop, release, rollback]`          | Faceted search          |#