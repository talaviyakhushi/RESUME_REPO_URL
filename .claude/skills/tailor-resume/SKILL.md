---
name: tailor-resume
description: Tailor resume.md to a specific job posting without fabricating anything. Read this before making any changes when asked to tailor the resume in this repository.
---

# Tailor Resume

You are tailoring the master resume in this repository (`resume.md`) to a
specific job posting supplied in the prompt. Follow every rule in this file.

## Process

1. Read `resume.md` in the repo root completely before writing anything. It is
   the single source of truth about the candidate.
2. Read the job posting in the prompt. List the top 5–8 requirements and
   keywords (skills, technologies, responsibilities, seniority signals).
3. Map each requirement to concrete evidence in `resume.md`. If there is no
   evidence for a requirement, it stays unmatched — do NOT invent evidence.
4. Write the tailored resume and a fit report to the output location below.
5. Never modify `resume.md` itself or delete anything outside your output
   folder.

## Output location convention

Write exactly two files, creating directories as needed:

```
jobs/{company-slug}/{role-slug}/resume.md
jobs/{company-slug}/{role-slug}/fit-report.md
```

Slugs are lowercase, non-alphanumeric runs replaced with single hyphens
(e.g. "Acme Corp" → `acme-corp`, "Senior Software Engineer" → `senior-software-engineer`).

## Tailoring approach

- **Reorder and emphasize, don't invent.** Move the most relevant experience
  and bullets to the top. Trim bullets that are irrelevant to this posting.
- **Keyword alignment.** Where the posting and the resume describe the same
  thing with different words, adopt the posting's phrasing — only when it is
  honestly equivalent (e.g. "CI/CD pipelines" for existing deploy-tooling
  work). Never adopt a keyword for something the candidate hasn't done.
- **Summary rewrite.** Rewrite the summary section to speak to this role,
  using only facts from `resume.md`.
- **Length.** Keep the tailored resume to roughly one page of markdown.

## ATS-friendly markdown rules

- Standard section headings: `## Summary`, `## Experience`, `## Skills`, `## Education`.
- One `#` H1 with the candidate's name at the top, contact info on the next line.
- Plain hyphen bullets; no tables, images, HTML, columns, or emoji.
- Spell out acronyms once where the posting uses the long form.
- Dates in `YYYY–YYYY` or `YYYY–present` form, consistent throughout.

## fit-report.md format

```
# Fit report: {Role} @ {Company}

## Strong matches
- {requirement} → {evidence from resume.md}

## Partial matches
- {requirement} → {closest adjacent experience, honestly framed}

## Gaps
- {requirement with no supporting evidence — listed, not papered over}

## Changes made
- {summary of what was reordered/rephrased and why}
```

## Hard boundaries — never violate these

- Never add a skill, tool, language, or framework that is not in `resume.md`.
- Never add an employer, title, project, or date range not in `resume.md`.
- Never add or change a metric (percentages, dollar amounts, team sizes,
  multipliers). Metrics may only be copied verbatim from `resume.md`.
- Never inflate seniority ("led" stays "led" only if `resume.md` says so).
- Never claim certifications, degrees, or publications not in `resume.md`.
- If the job is a poor fit, say so in `fit-report.md` — do not force a match.
