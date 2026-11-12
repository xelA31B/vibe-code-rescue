# AI App Doctor — Claude plugin

Your app was built with AI and now it's broken, or you're not sure it's safe to launch. AI App Doctor finds the cause, fixes it with the smallest safe change and proves it works.

## Skills

| Skill | What you get |
|-------|--------------|
| **vibe-rescue** | Diagnose and fix: failed builds and deploys (Vercel, Netlify, Lovable, Replit), missing env vars, broken imports, Supabase and auth errors, payment webhooks. Plain-language report with cause, fix and next steps. |
| **launch-check** | Read-only pre-launch audit: exposed secrets, open databases, auth and payment gaps, reliability and performance. Verdict 🟢/🟡/🔴 and a prioritized fix list. |

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
