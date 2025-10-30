---
title: Blameless post-mortems
created: 2025-10-30
updated: 2025-10-30
tags: [postmortem, reliability, incident-response, culture]
status: draft
summary: Running blameless post-mortems in engineering teams to learn from incidents without personal blame.
---

Nowadays it’s common sense to write blameless postmortems after incidents. Young SREs and DevOps engineers often speak passionately about their importance. Many learn the concept early on from books, talks, or Udemy courses. But that also means some of them have never experienced what it’s like when the opposite culture is in place.

A long time ago, a colleague of mine triggered a production outage by pressing V instead of Ctrl+V. That single character slipped into the code, and because back then we had no automated tests or CI/CD pipelines, it went straight to production.

The incident turned into a crisis. Meetings, panic, frustration, and eventually, blame. My colleague became the face of the outage, even though the real fragility was in the system itself. After all the drama, nothing changed: no new safeguards, no automation, no tests. Just the classic conclusion: “we all need to be more careful next time.”

It took me years to understand how much was lost in that reaction. A blameless culture doesn’t erase accountability; it redirects it toward learning and system design. Errors are inevitable, but the damage they cause depends on the resilience of the process around them.

People who only know blameless postmortems from training materials are lucky, it means they’ve never had to live through the version where mistakes are punished instead of studied.
