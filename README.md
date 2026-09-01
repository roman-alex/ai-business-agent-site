# AI Business Agent Site

Public, static website for **AI Business Agent**, an MVP SaaS product for AI-assisted business customer messaging. It provides the public and legal information needed for Meta Business Verification and Meta App Review.

The site has no backend, database, authentication, analytics, forms, or environment variables.

## Pages

- `/#/` — product overview
- `/#/privacy` — Privacy Policy
- `/#/terms` — Terms of Service
- `/#/data-deletion` — Data Deletion Instructions
- `/#/contact` — business contact information

Hash-based URLs are intentional: they make every route reliable on GitHub Pages without a server-side fallback.

## Local setup

Requirements: Node.js 22+ and npm. No environment variables are required.

```bash
npm install
npm run dev
```

Quality checks:

```bash
npm run typecheck
npm run lint
npm run build
```

The production output is written to `dist/`.

## Required business configuration

Before publishing, replace every placeholder in `src/config/business.ts`:

- `PLACEHOLDER_BUSINESS_LEGAL_NAME`
- `PLACEHOLDER_CONTACT_EMAIL`
- `PLACEHOLDER_WEBSITE_URL`

The config is shared by the footer and all legal/contact pages. Do not add secrets, Meta App Secrets, access tokens, private backend URLs, or tunnel URLs.

## Deploy to GitHub Pages

1. Create a GitHub repository named `ai-business-agent-site`.
2. Commit this project and push it to the repository's `main` branch.
3. In GitHub, open **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **GitHub Actions**.
5. The workflow in `.github/workflows/deploy-pages.yml` installs, builds, and deploys `dist/` on each push to `main`.
6. Check the **Actions** tab for the deployment result.
7. The resulting URL will normally be `https://<github-user>.github.io/ai-business-agent-site/`.
8. Set `businessConfig.websiteUrl` to that final URL, commit, and push again.

The Vite build uses relative asset paths, so it works under the repository subpath and remains ready for a future custom domain.

## URLs for Meta App Review

After deployment, replace `<domain-or-pages-url>` with the deployed base URL, without a trailing slash in the placeholder below:

- Website: `https://<domain-or-pages-url>/#/`
- Privacy Policy: `https://<domain-or-pages-url>/#/privacy`
- Terms of Service: `https://<domain-or-pages-url>/#/terms`
- Data deletion: `https://<domain-or-pages-url>/#/data-deletion`
- Contact: `https://<domain-or-pages-url>/#/contact`

For the default repository deployment, the values would be:

- Website: `https://<github-user>.github.io/ai-business-agent-site/#/`
- Privacy Policy: `https://<github-user>.github.io/ai-business-agent-site/#/privacy`
- Terms: `https://<github-user>.github.io/ai-business-agent-site/#/terms`
- Data deletion: `https://<github-user>.github.io/ai-business-agent-site/#/data-deletion`
- Contact: `https://<github-user>.github.io/ai-business-agent-site/#/contact`

Open each URL in a private browser window before submitting it to Meta.

## Moving to a custom domain later

1. Add the custom domain in **GitHub Settings → Pages**.
2. Add the DNS records shown by GitHub at your DNS provider.
3. Enable HTTPS after GitHub verifies the domain.
4. Update `businessConfig.websiteUrl`.
5. Update the website, Privacy Policy, Terms, Data Deletion, and Contact URLs in the Meta developer and business settings.

The hash routes remain valid on a custom domain. They can be migrated to clean paths later only if the host is configured with an SPA fallback.
