# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Tools for the owner's travel agent business. The repo holds both a small public website and personal/internal tools, separated by folder:

- `site/` — the public static site, deployed to Netlify. This is the **only** folder that gets published (`publish = "site"` in `netlify.toml`).
- `tools/` — personal/internal tools. Never deployed; anything here is private from the web but still visible to anyone who can read the Git repo.

Keep client data (names, passports, bookings, etc.) out of the repo entirely.

## Site

Plain static HTML/CSS with no build step, framework, or JavaScript dependencies.

- `site/contact.html` — trip inquiry form handled by **Netlify Forms**. Netlify detects it at deploy time via `data-netlify="true"`; the form's `name` attribute (`trip-inquiry`) must match the hidden `form-name` input. Spam is filtered with the `netlify-honeypot="bot-field"` field. On submit, Netlify redirects to `action="/thanks.html"`. Submissions appear in the Netlify dashboard under Forms. When adding or renaming form fields, every field needs a `name` attribute or Netlify won't store it.
- `netlify.toml` redirects `/` to `/contact.html` until a `site/index.html` exists.

## Running locally

- Preview the static pages: `python -m http.server 8000 --directory site`, then open http://localhost:8000/contact.html. Submitting the form here won't work because Netlify Forms only processes submissions on deployed sites.
- Netlify CLI (`npm install -g netlify-cli`): `netlify dev` serves the site using `netlify.toml`. Form submissions are still only captured on a real deploy (e.g. a deploy preview from a PR).
