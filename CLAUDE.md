# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-file static landing page for **daisy.alexvey.com** (Daisy — voice-first second brain for iPhone). No build system, no dependencies, no package manager. Everything lives in `index.html`: markup, inline `<style>`, inline JSON-LD structured data. Assets (favicons, og-image, manifest) sit next to it at the repo root.

The sibling app repo is `../daisy/`. This repo is marketing only.

## Editing & previewing

There is no dev server or build command. Edit `index.html` directly, then open it in a browser.

```bash
# Optional: serve locally so root-absolute paths (/og-image.png, /favicon.svg, etc.) resolve
python3 -m http.server 8000
# then visit http://localhost:8000
```

Opening the file via `file://` will break the icon and OG image previews because the `href`/`src` values are absolute (`/...`). Use a local server when verifying those.

## Deploy

GitHub Pages serves the repo root. `CNAME` pins the custom domain to `daisy.alexvey.com`. Pushing to the default branch publishes. No CI, no preview environments — every commit on the deployed branch is production. The full deploy/DNS recipe is in `README.md`.

## Form endpoint

The waitlist form is **already wired** to Formspree (`https://formspree.io/f/xojbdqkb`, see `index.html:774`). The README still describes a `REPLACE_WITH_YOUR_ENDPOINT` placeholder — that's stale; ignore it. If the endpoint ever needs to change, swap that single string.

## Page structure (top-down)

Read these in order to understand the narrative:

1. `<head>` — meta, OG/Twitter cards, JSON-LD `@graph` (WebSite, Person, SoftwareApplication, FAQPage). Keep these in sync when copy changes; the social card description and the `og:description` are *not* auto-derived.
2. Inline `<style>` block (lines ~125–593) — design system lives here. Custom properties at `:root` define the palette (`--ink`, `--coral`, `--butter`, etc.). The hero orb is a stack of pure-CSS layers (`.orb-ambient`, `.orb-rings`, `.orb-body`, `.orb-bars`) with keyframe animations; respect `prefers-reduced-motion` (already handled at the bottom of the stylesheet).
3. `<body>` sections in order: hero → `#how` → wedge → "where it's going" → who-it's-for → privacy → `#waitlist` → footer. Section anchors are linked from hero CTAs.

## Positioning — don't drift from it

Per the README, the page is deliberately a single-wedge bet: **"Daisy remembers who, where, when, and what every thought was about, so you can find any of them by any thread."** When changing copy, preserve that thread; the success signal is testers articulating the entity-graph wedge back unprompted. Don't soften it into a generic "AI notes app" pitch.

## Pre-launch reference

`../premortem-report-20260521-111536.html` (sibling to this repo) holds the pre-launch checklist. Re-read before each tag push or production change, per README guidance.

## Commit style

Commits follow `site(<scope>): <short imperative>`. Scopes seen in history: `hero`, `waitlist`, `orb`, `seo`, `footer`, plain `site` for repo-wide. Match this when adding commits.
