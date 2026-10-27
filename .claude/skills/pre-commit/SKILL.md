---
name: pre-commit
description: Review uncommitted code changes for bugs, naming, security, and consistency with project conventions before committing
---

# Pre-Commit Review

Review all uncommitted changes on the current branch and propose improvements before the code is committed.

## Step 1 — Gather changes

Run `git diff` (unstaged) and `git diff --cached` (staged) to collect everything that will be part of the next commit. If the user provides a specific scope (e.g., a package name or file path), narrow the diff accordingly.

Also run `git diff master...HEAD` to understand the full scope of the branch if there are prior commits.

## Step 2 — Review each changed file

For every modified file, read enough surrounding context to understand the change. Evaluate against these criteria (in priority order):

1. **Security vulnerabilities** — XSS via `innerHTML`/untrusted input, third-party scripts without HTTPS or SRI, `target="_blank"` without `rel="noopener noreferrer"`, committed secrets.
2. **Bugs** — broken links or asset paths, JS errors, layout breakage at mobile widths, `dist/` not rebuilt after `src/` changes.
3. **Accessibility** — missing `alt` text, heading order, contrast, keyboard focus.
4. **SEO** — `<title>`, meta description, Open Graph tags, `sitemap.xml`/`robots.txt` consistency.
5. **Consistency** — matches existing HTML/SCSS/JS conventions in the repo.
6. **Code simplicity** — dead CSS/JS, leftover template code, unnecessary complexity.
7. **Performance** — oversized images, render-blocking resources, unused assets.

## Step 3 — Present findings

Group findings by severity:

### Format

```
## Critical (must fix before commit)
- [file:line] Description of issue + suggested fix

## Warning (should fix)
- [file:line] Description of issue + suggested fix

## Suggestion (consider)
- [file:line] Description of improvement

## Looks good
- Brief summary of what was well-implemented
```

Rules:
- Be direct and specific — reference exact file paths and line numbers.
- For each issue, propose a concrete fix (code snippet or description), not just a complaint.
- If there are no issues in a severity level, omit that section.
- Do NOT pad findings to seem thorough — if the code is clean, say so.
- Do NOT suggest changes that are purely stylistic if the existing style is consistent with the codebase.

## Step 4 — Validate

Check that every file referenced by the changed HTML (CSS, JS, images, links) exists in the repo. If a `package.json` with a `build` script exists, run `npm run build` and report any failure as a **Critical** finding.

## Step 5 — Offer to fix

After presenting findings, offer to fix critical and warning issues automatically. Wait for user approval before making any changes.

## User input

$ARGUMENTS
