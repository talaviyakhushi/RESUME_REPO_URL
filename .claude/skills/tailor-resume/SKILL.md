---
name: tailor-resume
description: Tailor resume.md to a specific job posting without fabricating anything — fit report, honest tailored resume, change summary. Read this before making any changes when asked to tailor the resume in this repository.
---

# Tailor resume for one job

You are tailoring the master resume in this repository (`resume.md`) to a
specific job posting supplied in the prompt. Follow every rule in this file.

## Source of truth

- Read `resume.md` in the repo root completely before writing anything. It is
  the single source of truth about the candidate.
- JD requirements not supported by `resume.md` go in the fit report's
  **Do not add** section only — never into `tailored-resume.md`.

## Workflow

1. **Ingest** — Read the per-run prompt (company, role, URL, job description).
   Load `references/jd-extraction-taxonomy.md` and classify each JD requirement.
2. **Fit report** — Load `references/fit-report.md`. Pick the fit tier from that
   reference and include the required `**Verdict:**` line. Write
   `jobs/{company-slug}/{role-slug}/fit-report.md` with **Overall fit**,
   **Strong matches**, **Gaps**, **Do not add**.
3. **Tailor** — Load `references/keyword-alignment.md`,
   `references/markdown-resume-structure.md`, and
   `references/ats-formatting-and-parsing.md`. Write `tailored-resume.md` by
   rephrasing/reordering/emphasizing facts from `resume.md` only.
4. **Change summary** — Load `references/change-summary.md`. Document every
   meaningful edit in `change-summary.md`.
5. **Quality** — Skim `references/anti-patterns.md` and
   `references/agent-governance.md`. Optional: note plaintext test steps from
   `references/export-and-plaintext-test.md`.

## Output location convention

Write exactly three files, creating directories as needed:

```
jobs/{company-slug}/{role-slug}/fit-report.md
jobs/{company-slug}/{role-slug}/tailored-resume.md
jobs/{company-slug}/{role-slug}/change-summary.md
```

Slugs are lowercase, non-alphanumeric runs replaced with single hyphens; strip
legal suffixes (Inc, LLC, Ltd) from company names
(e.g. "Acme Corp Inc." → `acme-corp`, "Senior Software Engineer" → `senior-software-engineer`).

Never modify `resume.md` itself or delete anything outside your output folder.

## Bullet style — STAR method, always

Every bullet in `tailored-resume.md` follows STAR compressed to one line:
**outcome/result first, then the action and context that produced it.**

- Pattern: `<Result or problem solved> by <action> <context/stack>` — e.g.
  "Prevented duplicate-signup failures by handling Klaviyo HTTP 409 responses
  and re-routing existing profiles to the subscribe flow in NestJS."
- Never write plain "Built X using Y" activity bullets. If the master profile
  phrases something that way, reframe it around the problem it solved or the
  outcome it enabled.
- Results with numbers beat qualitative results — but ONLY use metrics that
  exist in `resume.md`. Never invent or extrapolate a number.
- When no metric exists, the result clause is qualitative but concrete
  (what became possible, what failure stopped happening).

## Tailoring approach

- **Reorder and emphasize, don't invent.** Move the most relevant experience
  and bullets to the top. Trim bullets that are irrelevant to this posting.
- **Keyword alignment.** Where the posting and the resume describe the same
  thing with different words, adopt the posting's phrasing — only when it is
  honestly equivalent (e.g. "CI/CD pipelines" for existing deploy-tooling
  work). Never adopt a keyword for something the candidate hasn't done.
  Full rules in `references/keyword-alignment.md`.
- **Summary rewrite.** Rewrite the summary section to speak to this role,
  using only facts from `resume.md`.
- **Length.** Keep the tailored resume to roughly one page of markdown.

## Hard boundaries — never violate these

- Never add a skill, tool, language, or framework that is not in `resume.md`.
- Never add an employer, title, project, or date range not in `resume.md`.
- Never add or change a metric (percentages, dollar amounts, team sizes,
  multipliers). Metrics may only be copied verbatim from `resume.md`.
- Never inflate seniority ("led" stays "led" only if `resume.md` says so).
- Never claim certifications, degrees, or publications not in `resume.md`.
- If the job is a poor fit, say so in `fit-report.md` with the Stretch tier —
  do not force a match.

See `references/anti-patterns.md` and `references/master-profile-contract.md`
for the full contract.
