---
name: vibe-rescue
description: >
  This skill should be used when the user's AI-built or no-code app is broken: "my Lovable app
  doesn't work", "Bolt build failed", "Vercel deploy fails", "Netlify build error", "login stopped
  working", "Supabase error", "Stripe payments not working", "white screen after deploy",
  "fix my vibe-coded app", or any bug in an app generated with Lovable, Bolt, v0, Cursor, Replit,
  Windsurf or similar tools. Also triggers on the same requests in Russian ("сломалось приложение",
  "не работает деплой", "ошибка сборки") or Hungarian.
metadata:
  version: "0.1.0"
---

# Vibe Code Rescue — diagnose and fix

Find the root cause of a bug in an AI-built app, fix it with the smallest safe change, and prove the fix works.

## Style rules

- Language of the user's request. Concise, professional, no filler.
- Assume the user is not a developer: explain cause and fix in plain words, one or two sentences each. Technical details go in a short "For developers" block.
- Never guess. State what you verified and how.

## Safety rules (always)

1. **Read before you change.** Do not modify files until the cause is identified.
2. **Work on a branch.** In a git repository, create `rescue/<short-topic>` before the first edit. Never commit directly to the main branch.
3. **No destructive actions without explicit confirmation:** deleting files or data, database migrations, force-push, changing production settings, rotating keys, deploying.
4. **Secrets:** never print a full key, token or password. Show at most the first 4 characters. Never commit secrets; if one is already in the repository, report it and recommend rotation — do not rotate it yourself.
5. **Minimal change:** fix the cause, do not refactor or restyle unrelated code.
6. **Stop and escalate** when the fix needs access you don't have (hosting dashboard, payment provider, DNS) or touches money, personal data or authentication logic in a risky way. Prepare a developer brief instead (see Step 6).

## Step 1 — Intake

Ask in one short message only for what is missing:

- What is broken, since when, and what changed just before (new feature, deploy, package update)
- Where it runs: hosting (Vercel, Netlify, Lovable, Replit…), database/auth (Supabase, Firebase…), payments (Stripe…)
- Access: is the project open here (Claude Code / local folder / connected repository)? If not, ask for the repository or for the exact error text, build log and screenshot.

## Step 2 — Reproduce and collect evidence

Use what is available, cheapest first:

- Build locally (`npm install` then `npm run build` or the project's build script) and capture the first real error, not the last line.
- Read hosting build/deploy logs if the user can paste them or a connected tool provides them.
- Recent git history: `git log --oneline -20` and the diff of the last commits before the breakage.
- Browser console / network errors described or pasted by the user.

## Step 3 — Check the usual suspects

Go through `references/common-failures.md` for the stack involved. Most AI-built app failures fall into: missing or misnamed environment variables, imports or components referenced but not imported, case-sensitive file paths that work locally but fail on Linux hosts, dependency/version conflicts, wrong build output settings, Supabase row-level security or wrong keys, auth redirect URLs, Stripe webhook secrets and test/live key mix-ups.

## Step 4 — Fix

- Explain the cause in one plain sentence and the planned change in one sentence before editing.
- Make the minimal change on the rescue branch.
- Never paste secrets into code; use environment variables and tell the user exactly which variable to set and where (hosting dashboard path), without revealing values.

## Step 5 — Verify

- Re-run the build and, if present, tests and linter. Show the result (pass/fail), not just "should work".
- If the fix can only be verified on the hosting platform, list the exact steps for the user to confirm (redeploy, open URL, expected result).
- Commit on the rescue branch with a clear message. Ask before pushing; never merge or deploy without confirmation.

## Step 6 — Report

Use this format, in the user's language:

```
**Problem:** what the user saw
**Cause:** one plain sentence
**Fix:** what was changed (branch: rescue/…)
**Verified:** build ✅/❌ · tests ✅/❌/none · what still needs checking on the hosting side
**Your next step:** 1–3 concrete actions (merge, set variable X in Vercel → Settings → Environment Variables, redeploy)
**Also noticed:** other risks found, max 3, one line each (offer `launch-check` for a full audit)

For developers: files changed, commands run, error before/after (short)
```

If escalating, write a **developer brief** instead: symptom, evidence collected, likely cause, what was ruled out, access needed, suggested fix — so any developer can pick it up in minutes.
