---
title: "Incident Management Temlate"
owner: "joe.southin@gmail.com"
reviewers: ["joe.southin@gmail.com"]
status: approved
first_published: 2025-05-29
last_reviewed: 2025-05-29
next_review_due: 2026-05-29   # 12-month cadence
tags: [meta, im, template]
---

|Field|Example Detail|
|---|---|
|Incident Manager|{Incident Manager}|
|Status|Closed|
|Date|03/14/2023|
|Document ID|IM-310|
|Severity|`SEV-1` · `SEV-2` · `SEV-3`|
|Overview|Include a short sentence or two summarizing the root cause, timeline summary, and the impact. E.g. `"On the morning of August 99th, we suffered a 1 minute SEV-1 due to a runaway process on our primary database machine. This slowness caused roughly 0.024% of alerts that had begun during this time to be delivered out of SLA."`|
|Root Cause|Include a description of any conditions that contributed to the issue. If there were any actions taken that exacerbated the issue, also include them here with the intention of learning from any mistakes made during the resolution process.|
|Resolution	|Include a description what solved the problem. If there was a temporary fix in place, describe  that along with the long-term solution.|
|Impact	|Brief descripttion of impact|
|Responders|	List all involved and their role in finding root cause and resolving the incident|
|Slack	|An IM-* slack channel should be opened during the Icident. Add the information here. |
|Timelines|"Some important times to include: (1) time the root cause began, (2) time of the page, (3) time that the status page was updated (i.e. when the incident became public), (4) time of any significant actions, (5) time the SEV-2/1 ended, (6) links to tools/logs that show how the timestamp was arrived at."|
|Time to discovery||
|Time to resolution||
|Time to close||