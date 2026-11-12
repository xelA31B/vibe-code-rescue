---
name: launch-check
description: >
  This skill should be used when the user asks "is my app ready to launch", "audit my Lovable app",
  "security check before launch", "review my vibe-coded app", "pre-launch checklist", "what could go
  wrong with my app", "is my Supabase secure", or wants a health and security audit of an app built
  with Lovable, Bolt, v0, Cursor, Replit or similar tools. Also triggers on the same requests in
  Russian ("готово ли приложение к запуску", "проверь безопасность приложения") or Hungarian.
metadata:
  version: "0.1.0"
---

# Launch Check — pre-launch audit for AI-built apps

Audit an AI-built app for the problems that break launches or leak data, and give a prioritized fix list.

## Style rules

- Language of the user's request. Concise, professional, no filler. Tables over paragraphs.
- Plain words for the main report; technical detail only in the "For developers" column or appendix.
- Report only what you verified. Mark unverifiable items as **not checked** with what is needed to check them.
- Read-only by default: do not change code, settings or data during the audit. Offer fixes afterwards (`vibe-rescue`).
- Never print full secrets; show at most the first 4 characters.

## Step 1 — Scope

Ask only for what is missing: access to the code (open project, repository or connected GitHub), live URL, stack (hosting, database/auth, payments), and whether real users or payments are already live.

## Step 2 — Run the checks

Use `../vibe-rescue/references/common-failures.md` as the checklist. Cover these areas:

| Area | What to check |
|---|---|
| Build & deploy | Production build passes; latest deploys succeed; env vars set for production |
| Secrets | No keys/tokens in code, git history, client bundle or tracked config (`.env`, `supabase/.temp`) |
| Data access | Database row-level security on; no admin/service keys in frontend; storage buckets private where needed |
| Authentication | Production redirect URLs; protected routes enforce auth server-side |
| Payments | Live keys and webhook configured; nothing unlocks without a verified webhook |
| Reliability | Error handling and user-facing error messages; no debug mode in production |
| Performance | Image sizes, initial load, obvious slow queries |
| Basics | HTTPS, custom domain redirects, privacy policy/terms if collecting data, 404 page |

## Step 3 — Report

```
# Launch Check — [App] · [date]

**Verdict:** 🟢 Ready / 🟡 Launch after fixes / 🔴 Do not launch — one-line reason

## Critical (fix before launch)
| # | Issue | Why it matters | Fix | Effort |

## Important (fix soon)
| # | Issue | Why it matters | Fix | Effort |

## Passed
- one line per area that is fine

## Not checked
- item — what is needed to check it

For developers: evidence (file:line, setting, command output), max 1 line per issue
```

Verdict rule: 🔴 if any secret is exposed, data is publicly writable or payments can be bypassed; 🟡 if any other critical item exists; otherwise 🟢.

Close with one line offering to fix the critical items now with `vibe-rescue`, one at a time, on a separate branch.

## Recurring run

At the end of the report, offer a recurring run. Recommended cadence: before every release, and monthly for apps that are already live.

Let the user choose their own schedule. Ask in one short message, with the recommendation pre-filled:

- **Frequency:** daily · weekly · every 2 weeks · monthly · quarterly · custom
- **Day:** e.g. Monday, Friday, 1st of the month
- **Time and time zone:** e.g. 09:00 Europe/Budapest (use the user's time zone if known)
- **Delivery:** in this chat, a new chat, or a document

If the environment offers scheduled tasks (a scheduling tool is available), create the task only after the user confirms these choices. Write the scheduled prompt so it is self-contained: what to check (project, repository or company), which skill to run, the report language, and where to deliver the result. Confirm what was scheduled in one line. The user can change or cancel the schedule at any time; when asked, update or remove it.

If no scheduling tool is available, state the chosen or recommended cadence and suggest a calendar reminder.
