# Common failures in AI-built apps

Check the items that match the user's stack. Verify each against the actual code, logs or configuration before concluding.

## Build and deploy (Vercel, Netlify, Cloudflare Pages, Lovable, Replit)

| Symptom | Likely cause | How to verify |
|---|---|---|
| Builds locally, fails on host | Case-sensitive import path (`./Header` vs `./header.tsx`) | Compare import paths with real file names |
| `X is not defined` / `Cannot find name` | Component or function used but not imported (common after AI edits, e.g. `<Link>` without `import Link`) | Search the file for the symbol and its import |
| `Module not found` | Package missing from `package.json`, or installed only locally | Check `package.json` and lockfile |
| Type errors only in CI | Host runs strict type check (`next build`), local dev does not | Run the production build locally |
| Build passes, site blank | Wrong output directory or framework preset; env var missing at build time | Hosting build settings; browser console |
| Every deploy fails since commit X | Error introduced in that commit | `git diff` of that commit; rebuild previous commit |
| Env var undefined in browser | Client-side vars need the framework prefix (`NEXT_PUBLIC_`, `VITE_`) | Compare names in code vs hosting settings |
| Works in preview, fails in production | Variable set only for Preview environment | Hosting env settings per environment |
| Lockfile conflicts | Mixed package managers (npm + pnpm/yarn lockfiles) | List lockfiles in repo root |
| Node version errors | Host Node version differs from local | `engines` field / hosting Node setting |

## Supabase / Firebase

| Symptom | Likely cause | How to verify |
|---|---|---|
| Data visible to everyone / anyone can edit | Row Level Security disabled or policies allow all | Table RLS status and policies |
| Empty results though data exists | RLS enabled but no policy for the role | Policies for `anon` / `authenticated` |
| Admin powers in the browser | `service_role` key used in frontend code | Search client code for the key variable |
| Project details committed | `supabase/.temp`, `.env`, config files tracked in git | `git ls-files` for these paths; check `.gitignore` |
| Auth works locally, not in production | Site URL / redirect URLs not set for the production domain | Supabase Auth URL configuration |

## Authentication

- Redirect loop or "invalid redirect": callback URL missing in provider settings.
- Session lost on refresh: cookies blocked by domain mismatch (www vs non-www), or tokens kept only in memory.
- OAuth works for owner only: app still in "testing" mode at the provider.

## Payments (Stripe and similar)

- Payments succeed but nothing unlocks: webhook not configured for production URL, or wrong webhook signing secret.
- Works in test, fails live: live keys / live webhook secret not set, or test price IDs in code.
- Secret key in frontend code: critical — report and recommend rotation.

## Security quick scan

- Secrets in repository history or client bundle (API keys, tokens, `.env`).
- Public storage buckets with private files.
- Admin routes without auth checks.
- Forms without server-side validation or rate limiting.
- Debug mode or verbose error pages in production.

## Performance

- Huge images without optimization; all data fetched on page load; no pagination; database queries inside loops.
