---
name: audit
description: Run a thorough codebase audit covering security, scalability, maintainability, and code quality — report weaknesses and strengths honestly
---

# Codebase Audit

Perform a senior-level audit of this codebase. The goal is to find real problems and actionable improvements — not to be encouraging.

## Scope

If the user specifies an area (e.g., `src/scss`, `src/js`, `index.html`), scope the audit to that area. Otherwise, audit the full site.

This is a static GitHub Pages site (`index.html`, `src/` sources compiled into `dist/`, `assets/`, `sitemap.xml`, `robots.txt`).

## Step 1 — Explore

Build a picture of:
- Directory structure and how `src/` maps to `dist/`
- Build tooling (see `package-sample.json`) and whether `dist/` is in sync with `src/`
- Third-party scripts, stylesheets, fonts, and CDNs loaded by the pages
- SEO and crawl configuration (`sitemap.xml`, `robots.txt`, meta tags)

## Step 2 — Audit categories

Evaluate each category. For every finding, cite specific files and line numbers.

### Security
- Third-party scripts: loaded over HTTPS, pinned versions, Subresource Integrity (`integrity` + `crossorigin`)?
- Outbound links: `target="_blank"` without `rel="noopener noreferrer"`?
- Secrets or personal data committed to the repo (API keys, emails meant to be private)?
- Inline handlers or `innerHTML` with untrusted input in `src/js`?

### Performance
- Image sizes and formats (oversized PNG/JPG, missing `width`/`height`, no lazy loading)?
- Render-blocking CSS/JS, unminified or unused assets in `dist/`?
- Font loading strategy?

### Accessibility & SEO
- Semantic HTML, heading order, `alt` text, colour contrast, keyboard navigation?
- `<title>`, meta description, Open Graph tags, canonical URL, `lang` attribute?
- `sitemap.xml` and `robots.txt` correct and consistent with the live URL?

### Maintainability & Code Quality
- Dead CSS/JS, leftover template code, duplicated styles?
- `dist/` artifacts drifting from `src/`?
- Broken links or references to missing files?
- Outdated or vulnerable dependencies in `package-sample.json`?

## Step 3 — Report

Present the audit as a structured report:

```
## Audit Summary
One paragraph: overall health assessment.

## Strengths
- Bullet list of what the codebase does well (be specific, not generic)

## Critical Issues (fix now)
- [Category] file:line — Description + impact + recommended fix

## Important Issues (fix soon)
- [Category] file:line — Description + impact + recommended fix

## Improvements (backlog)
- [Category] file:line — Description + benefit

## Metrics
- Total page weight (HTML + CSS + JS + images)
- Number of third-party requests and how many lack SRI
- Images missing `alt` text
```

Rules:
- Be brutally honest. The user explicitly wants real problems, not encouragement.
- Every finding must cite a specific file and line — no vague observations.
- Prioritize findings by impact (security > accessibility > performance > maintainability > style).
- If an area is genuinely well-done, say so briefly — but don't pad the strengths section.
- Propose actionable fixes, not just problems.

## User input

$ARGUMENTS
