# AnyOutreach

**Cold outreach that runs on the AI assistant you already have.**

AnyOutreach is an agent-native skill pack that turns any coding assistant (ZCode, Claude Code, Codex CLI, Cursor, or anything that loads markdown skills) into a cold-email pipeline: it profiles your prospects, writes personalized first emails, queues them in a plain-text outbox you approve, and drafts the replies. You bring the agent and the prospect list. No API keys, no per-token bills, no lock-in to one vendor's CLI.

```
you:     run outreach for this list
agent:   read outreach/persona.md ... 40 prospects in scope, 22 fit email
agent:   profiled 10 so far. Batch 1 queued in outreach/OUTBOX.md (10 drafts)
you:     (reads the drafts, fixes one, approves the batch)
agent:   marked approved. Sending is yours until a mailbox is configured.
later:   (a prospect replies; you paste it)
agent:   objection: price. Draft queued. Prospect 2 said "remove me": closed, permanently.
```

## Why this exists

The strongest open-source cold-email agent, [Harvey](https://github.com/ethanplusai/harvey), runs its brain through the `claude` CLI (or a pinned Codex build). That couples your outreach to one vendor's subscription and one provider's plumbing. AnyOutreach takes Harvey's method (MIT, credited below) and makes the *agent itself* the runtime, which buys three things:

- **Any assistant.** If your tool can read a SKILL.md and fetch a URL, it can run this. Switching agents costs you nothing.
- **Your list, not its list.** Stock discovery engines find what they find; you point this at your own CSV, crawl, or CRM export.
- **Approval-first by construction.** The outbox is a markdown file. Nothing sends unless you flip its status, and sending itself is bring-your-own (SMTP script, manual paste, or your sequencer) until you wire it.

What you give up vs. stock Harvey: automated discovery, built-in mail providers, and the web dashboard. If you want those and have a Claude Pro/Max plan, use Harvey. This is the portable 80%.

## Install

The pack is one skill. Copy it wherever your agent keeps skills:

| Agent | Destination |
|---|---|
| ZCode | `~/.agents/skills/cold-outreach/` |
| Claude Code | `~/.claude/skills/cold-outreach/` |
| Codex CLI | `~/.codex/skills/cold-outreach/` |
| Others | put `SKILL.md` + `references/` wherever your agent loads instructions from, or paste the SKILL.md body into your AGENTS.md |

```bash
git clone https://github.com/AhmedHassan21/anyoutreach.git
cp -r anyoutreach/skill/* ~/.agents/skills/cold-outreach/   # or your agent's dir above
```

## Use

1. In your project, ask the agent to "set up outreach". It interviews you (or reads your site) and writes `outreach/persona.md` from `references/persona-template.md`. This file is the only source of truth for product claims.
2. Point it at a prospect list (CSV with company, site, category, city is enough).
3. It profiles prospects, drafts email 1 per prospect into `outreach/OUTBOX.md`, and stops. You edit and flip `status: draft` to `approved`.
4. Non-responders get email 2 (new angle) and a short email 3 on the schedule in `references/method.md`, then a clean breakup.
5. Replies get classified and drafted per `references/replies.md`. Opt-outs close the prospect permanently, no exceptions.

Sending: manual until you attach a mailbox. The persona template documents the deliverability checklist (secondary domain, warmup, 50/day cap) that gates real volume.

## What's in the box

```
skill/SKILL.md                    the workflow + hard gates
skill/references/method.md        writing rules, sequence, ban list, reply triggers
skill/references/replies.md       reply classification and drafting
skill/references/persona-template.md
examples/                         fictional persona + sample batch
```

## License and credits

MIT. The outreach method, writing rules, and reply-handling guidance are adapted from [ethanplusai/harvey](https://github.com/ethanplusai/harvey) by Ethan Rogers (MIT). Go star the original; this project would not exist without it.

No affiliation with harvey.ai (the legal AI company). The name AnyOutreach was chosen on purpose.
