# is-an.org — Free Subdomain Service

A single-page, fully static application page where users can request a free `yourname.is-an.org` subdomain for open-source projects, personal projects, and non-profit organizations.

## How it works

Pure frontend + email. No backend, no database, no third-party services:

1. The applicant fills in a form: desired subdomain, name, contact email, project type, description, and DNS records.
2. Clicking **Submit** opens their mail app with a pre-filled email addressed to `contact@is-an.org`.
3. The administrator manually reviews the request, adds the DNS records if approved, and replies to the applicant.

## Project structure

```
.
├── index.html   # The application page (the only file you need)
└── README.md
```

## Features

- Subdomain input with silent cleanup — lowercases, strips invalid characters, and merges consecutive hyphens automatically
- Multiple DNS records per request — **A / AAAA / CNAME / NS / MX / TXT**
- **NS records are recommended**: delegating DNS management to the applicant's own provider (e.g. Cloudflare's free plan) lets them manage their own records without contacting you
- **Copy Application** button for users without a configured mail client (e.g. on mobile) — they can paste the content into any webmail
- Fully responsive, mobile-friendly

## Deploy

The page runs on any static hosting platform, for example:

- **Cloudflare Pages**
- **GitHub Pages**
- **Vercel / Netlify**
- **Any Nginx or object-storage static site**

### Cloudflare Pages example

1. Create a Pages project in the [Cloudflare Dashboard](https://dash.cloudflare.com).
2. Connect this repository (or upload `index.html` directly).
3. Build settings: leave Build command empty and set Build output directory to `/`.
4. After deploying, add the custom domain `is-an.org`.

## Configuration

To change the recipient email, edit the `RECIPIENT` variable in `index.html`:

```javascript
var RECIPIENT = 'contact@is-an.org';
```

## Administrator workflow

1. Read the incoming application email.
2. Approve or reject based on the service rules shown on the page.
3. If approved, add the requested DNS record(s) for the subdomain in your DNS provider (e.g. Cloudflare):
   - **NS record** — add the applicant's nameservers; the applicant then manages everything else themselves.
   - **A / AAAA / CNAME** — add the record pointing to the target IP or domain.
4. Reply to the applicant with the result.

## Notes

- Emails are sent via `mailto:` from the applicant's local mail client — nothing goes through a server.
- The page cannot check whether a subdomain is already taken; that is part of the manual review.
- Domains that are left unmaintained or used for prohibited purposes may be reclaimed.

## License

MIT
