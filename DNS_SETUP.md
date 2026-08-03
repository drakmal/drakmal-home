# drakmal.com — DNS & Deployment Reference

## Hosting

- **Landing page**: `index.html` in this repo, hosted on GitHub Pages
  ([github.com/drakmal/drakmal-home](https://github.com/drakmal/drakmal-home))
- Custom domain `drakmal.com` is set via the `CNAME` file in the repo root
- HTTPS is enforced; certificate covers `drakmal.com` and `www.drakmal.com`, auto-renews via GitHub (issued cert expires 2026-10-31)

## DNS records at Porkbun

| Type | Host | Answer / Target | Purpose |
|---|---|---|---|
| A | (root) | 185.199.108.153 | GitHub Pages — apex domain |
| A | (root) | 185.199.109.153 | GitHub Pages — apex domain |
| A | (root) | 185.199.110.153 | GitHub Pages — apex domain |
| A | (root) | 185.199.111.153 | GitHub Pages — apex domain |
| CNAME | www | drakmal.github.io | GitHub Pages — `www` redirect to apex |
| CNAME | acdmeasles | acdmeasles.netlify.app | ACD Measles Data Collection Form (Netlify) |
| CNAME | conference-finder | 747d40538a80e68c.vercel-dns-017.com | Conference Finder (Vercel) |
| CNAME | relocate | ca156c574589803f.vercel-dns-017.com | Relocate and Stay Options (Vercel) |
| CNAME | * (wildcard) | uixie.porkbun.com | Catch-all for undefined subdomains → Porkbun parking page |
| MX | (root) | fwd1.porkbun.com (prio 10), fwd2.porkbun.com (prio 20) | Porkbun email forwarding |
| MX | send | feedback-smtp.ap-northeast-1.amazonses.com | Amazon SES outbound mail (send.drakmal.com) |
| TXT | resend._domainkey | (DKIM key) | DKIM signing for Resend email service |
| TXT | (root) | v=spf1 include:_spf.porkbun.com ~all | SPF for Porkbun-forwarded mail |
| TXT | send | v=spf1 include:amazonses.com ~all | SPF for Amazon SES |
| TXT | subdomain-owner-verification | (verification token) | Third-party subdomain ownership verification |
| TXT | _acme-challenge | (x2 challenge tokens) | Let's Encrypt/ACME certificate validation for subdomains |
| TXT | _dmarc | v=DMARC1; p=none; | DMARC policy (monitoring only, no enforcement) |

**Do not delete** the wildcard, MX, or TXT records — they support email delivery/auth and cert
validation for the other subdomains. Only the old root `ALIAS drakmal.com → uixie.porkbun.com`
record was removed (replaced by the 4 A records above) to stop the domain from showing Porkbun's
default parking page.

## Project links (as shown on the homepage)

| Button | URL | Backing host |
|---|---|---|
| Communicable Disease Dashboard | https://drakmal.github.io/comm_dss_dashboard/ | GitHub Pages |
| ACD Measles Data Collection Form | access restricted, not publicly linked | Netlify |
| Relocate and Stay Options | https://relocate.drakmal.com/ | Vercel |
| Conference Finder | https://conference-finder.drakmal.com/ | Vercel |

## Adding a new project later

1. Point its subdomain at wherever it's hosted (add a DNS record at Porkbun, same pattern as above).
2. Add a new `<div class="card">` block to `index.html` (see [README.md](README.md)).
3. Commit and push — GitHub Pages redeploys automatically.
