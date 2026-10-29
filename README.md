# Shonen Siege Tower Defense

This repository hosts Shonen Siege V3.5 at:

https://shonen-siege-tower-defense.github.io/

## Deployment
- Hosted free with GitHub Pages.
- Build command: `npm install && npm run build`.
- GitHub Actions builds and deploys from the `main` branch.
- Vite is configured with `base: '/'` for a root-level organisation website.

## Important notes
- The original repository `ashplayz25xx1-cmd/Shonen-SiegeV3` remains unchanged as a backup.
- This repository contains a clean source snapshot; it does not preserve the original commit history.
- Supabase Auth redirect allow-list must include this new website URL before confirmation, password reset, or Google OAuth redirects will complete on this host.
- Keep any Supabase service-role or secret keys out of client-side files. Only the browser-safe publishable key belongs in `src/backend-config.js`.
