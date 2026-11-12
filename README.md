# Doctor FixCode — Claude plugin

Your app was built with AI and now it's broken, or you're not sure it's safe to launch. Doctor FixCode finds the cause, fixes it with the smallest safe change and proves it works.

## Install

**Claude app (web, desktop):** Plugins → add a marketplace from a GitHub repository → `xelA31B/vibe-code-rescue` → install **Doctor FixCode**. Once approved in the Claude directory, search for **Doctor FixCode** in Plugins.

**Claude Code (VS Code or terminal):**

```
/plugin marketplace add xelA31B/vibe-code-rescue
/plugin install doctor-fixcode@doctor-fixcode
```

## Skills

| Skill | What you get |
|-------|--------------|
| **vibe-rescue** | Diagnose and fix: failed builds and deploys (Vercel, Netlify, Lovable, Replit), missing env vars, broken imports, Supabase and auth errors, payment webhooks. Plain-language report with cause, fix and next steps. |
| **launch-check** | Read-only pre-launch audit: exposed secrets, open databases, auth and payment gaps, reliability and performance. Verdict 🟢/🟡/🔴 and a prioritized fix list. |

## Commands

Type `/` in Claude and pick a command:

| Command | What it does |
|---|---|
| `/app-launch-check [project or URL]` | Pre-launch security and health audit of an app |
| `/fix-app [what is broken]` | Diagnose and fix a broken AI-built app |

## How to use

Works best in Claude Code (VS Code or terminal) with the project open. In the Claude app, connect the GitHub repository or paste error logs.

- "My Vercel deploy keeps failing — fix it"
- "Мое приложение из Lovable не логинит пользователей"
- "Is my app ready to launch?"

## Safety by default

- Reads first, changes only after the cause is found
- Works on a separate `rescue/…` branch; never commits to main
- No deletions, migrations, force-push, key rotation or deploys without your explicit confirmation
- Never prints full secrets

## License

MIT
