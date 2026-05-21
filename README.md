# Daisy landing page

Static HTML for `daisy.alexvey.com`. Single file, no build step, no deps.

## Files

- `index.html` — the page
- `CNAME` — github pages custom domain pointer

## Before going live

**Wire the waitlist form.** The form points to a placeholder. Pick one:

1. **Formspree** (easiest) — sign up at https://formspree.io, create a form, copy the endpoint, replace `https://formspree.io/f/REPLACE_WITH_YOUR_ENDPOINT` in `index.html`.
2. **Buttondown** — change form action to `https://buttondown.email/api/emails/embed-subscribe/YOUR_USERNAME` and the input `name` to `email`.
3. **ConvertKit / MailerLite / etc.** — most provide a one-line `action=` swap.

While the placeholder is in place, the submit button posts to a non-existent endpoint and the user gets an error. Swap before launch.

## Deploying to github pages

1. Push this directory to a github repo (the existing `daisy` repo is fine; either move these files to `/docs` or use a separate `gh-pages` branch).
2. In the repo settings → Pages, choose the branch + folder.
3. Add an A or CNAME DNS record for `daisy.alexvey.com` pointing at github pages (`alexvey.github.io` or the four github A records).
4. Github reads the `CNAME` file in this directory and configures the domain.
5. Enable "Enforce HTTPS" once the cert provisions (a few minutes).

If hosting under `/docs`:

```bash
mkdir -p ../docs
mv index.html CNAME ../docs/
git add ../docs && git commit -m "site: add daisy.alexvey.com landing"
git push
```

In repo Settings → Pages → set source to `main` branch, `/docs` folder.

## What's being stress-tested

This page deliberately leads with one wedge sentence: **"Daisy remembers who, where, when, and what every thought was about, so you can find any of them by any thread."**

The signal worth watching: signup rate, and (if you reply to subscribers) what they say in the reply. If 5+ of 10 testers can articulate the entity-graph wedge back to you unprompted, the positioning lands. If they all say "looks beautiful" and never use the verb "remember" or "connect," the wedge isn't landing and the page needs another pass.

The pre-launch checklist that the premortem produced lives in `../premortem-report-20260521-111536.html`. Re-read it before each tag push.
