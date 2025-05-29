---
title: "Front-Matter Schema"
owner: "joe.southin@gmail.com"
reviewers: ["joe.southin@gmail.com"]
status: approved
first_published: 2025-05-29
last_reviewed: 2025-05-29
next_review_due: 2026-05-29   # 12-month cadence
tags: [meta, docs]
---


# JSON Schema (enforced by CI)

```yaml
type: object
required: [title, owner, last_reviewed, next_review_due]
properties:
  title:  {type: string, minLength: 3}
  owner:  {type: string, pattern: '^[\\w.+-]+@[\\w.-]+$'}
  status: {type: string, enum: [draft, approved, deprecated]}
  last_reviewed:  {type: string, format: date}
  next_review_due: {type: string, format: date}
  tags:
    type: array
    items: {type: string}
additionalProperties: true
```

## Change process
PRs modifying the schema need **Docs Guild** + affected TL approval; CI re-lints repo.

## Common failures
| Message            | Cause            | Fix            |
|--------------------|------------------|----------------|
| enum error         | `Approved` caps  | use lowercase  |
| date format        | `29-05-2025`     | `YYYY-MM-DD`   |