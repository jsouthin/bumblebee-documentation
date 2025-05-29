---
title: "MVP Design Principles"
owner: "joe.southin@gmail.com"
reviewers: ["joe.southin@gmail.com"]
status: approved
first_published: 2025-05-29
last_reviewed: 2025-05-29
next_review_due: 2026-05-29   # 12-month cadence
tags: [mvp]
---

|MVP Design Principle|One-liner Summary|Description|
|--|--|--|
|🧩 **Design for Extensibility**|`“Structure systems so they can grow with minimal friction.”`| Use separate frontend/backend repos and APIs<br>Modularize components to enable parallel workstreams|
|🔁 **Design for Replaceability**|`“Avoid lock-in — make components easy to swap.”`|Abstract DB access using a repository pattern<br>Define interfaces around key system boundaries|
|⚡ **Do the Simplest Thing That Works**|`“Solve today’s problem, not imaginary future ones.”`|Prefer clarity over cleverness<br>Avoid speculative features or premature optimization|
|☁️ **Bias Toward Managed Services & Tools**|`“Optimize for focus and speed, not reinventing infrastructure.”`|Use AWS RDS, Cognito, CloudWatch, etc. where possible<br>Choose mature, widely adopted libraries and frameworks|
|🧠 **Build for Learning, Not Perfection**|`“MVP is for feedback, not forever.”`|Instrument early with logs, metrics, and basic analytics<br>Prioritize features that give user signals over polish|


