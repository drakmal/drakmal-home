# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single self-contained static HTML page (`index.html`) that serves as the landing page for
drakmal.com. It's a dashboard-style grid of cards, one per project, each linking out to that
project's own subdomain or hosted URL. There is no build step, framework, or package manager —
just plain HTML with an inline `<style>` block.

## Commands

None. Edit `index.html` directly and open it as a local file (`file://...`) in a browser to
preview — no dev server, bundler, or test suite exists or is needed for this project.

## Architecture

- `index.html` — the entire site. All CSS is inline in a `<style>` tag; there are no external
  assets, fonts, or CDN dependencies. Colors are defined as CSS custom properties on `:root` with
  a `prefers-color-scheme: dark` override, so the page adapts to the visitor's OS theme
  automatically.
- Each project is a `<div class="card">` inside `<main class="grid">` — icon, title, one-line
  description, and a button (`<a target="_blank" rel="noopener">`) linking to that project's own
  URL. To add/remove/relabel a project, edit these card blocks directly; there's no data file or
  templating layer.
- `CNAME` — required by GitHub Pages to serve the custom apex domain `drakmal.com`. Must contain
  exactly `drakmal.com` with no other content.
- Deployment: pushing to `main` on [github.com/drakmal/drakmal-home](https://github.com/drakmal/drakmal-home)
  auto-redeploys via GitHub Pages (legacy build). No CI config exists or is needed.
- DNS/hosting details for drakmal.com and its project subdomains (which records exist, what each
  is for, and why) are documented in [DNS_SETUP.md](DNS_SETUP.md) — read that before touching any
  DNS-related record, since several subdomains point to other services (Netlify, Vercel) and there
  are email (MX/SPF/DKIM/DMARC) records that must not be disturbed.
