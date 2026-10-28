---
name: cold-outreach
description: >
  Run an approval-first cold-email outreach pipeline for any product: profile prospects,
  write personalized first emails following the Harvey method (one observation, one
  question, under 75 words, no AI tells), queue them in a project-local OUTBOX for
  human approval, and draft replies when responses arrive. Use for requests like
  "write cold emails for this list", "run outreach", "draft our email campaign",
  or "handle these prospect replies". Nothing sends without explicit human approval.
license: MIT
compatibility: Works in any project. Sending requires an SMTP mailbox configured by the user; the skill itself only writes drafts.
metadata:
  author: user
  origin: Adapted from ethanplusai/harvey (MIT) — method and rules; implementation is agent-native.
---

# cold-outreach

This file is the discovery entrypoint when the whole repository is cloned
into a skills folder. The canonical skill lives one level down.

**Read [skill/SKILL.md](skill/SKILL.md) and follow it.** Candidate or user
data never belongs in this repository.
