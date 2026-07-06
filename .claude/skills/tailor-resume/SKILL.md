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
   `references/markdown-resume-structure.md`,
   `references/ats-formatting-and-parsing.md`, and
   `references/recruiter-heuristics.md`. Build the recruiter-side risk map
   internally, then write `tailored-resume.md` by rephrasing/reordering/
   emphasizing facts from `resume.md` only. Respect the fixed bullet counts
   in `references/markdown-resume-structure.md` (Forty7: 3, NJIT RA: 3,
   BNP: 3, each project: 3).
4. **Change summary** — Load `references/change-summary.md`. Document every
   meaningful edit in `change-summary.md`.
4b. **LaTeX output** — Read `templates/resume-template.tex` and write
   `tailored-resume.tex` in the same job folder: fill the template's
   placeholder slots (summary, skills lines, stack lines, bullets, project
   block) with the exact content of `tailored-resume.md`. Rules:
   - Escape LaTeX special characters: `%` → `\%`, `&` → `\&`, `#` → `\#`,
     `$` → `\$`, `_` → `\_`.
   - Date ranges use `--` (e.g. `Jan 2026 -- May 2026`).
   - Do not alter the template's preamble, custom commands, or spacing —
     content goes into the marked slots only.
   - Keep heading structure: company bold via `\resumeExpHeading`, stack via
     `\resumeStack`, bullets via `\resumeItem`.
5. **Quality** — Skim `references/anti-patterns.md` and
   `references/agent-governance.md`. Run the six-second clarity gate and the
   ASCII normalization check from `references/recruiter-heuristics.md` on
   `tailored-resume.md`. Optional: note plaintext test steps from
   `references/export-and-plaintext-test.md`.

## Output location convention

Write exactly four files, creating directories as needed:

```
jobs/{company-slug}/{role-slug}/fit-report.md
jobs/{company-slug}/{role-slug}/tailored-resume.md
jobs/{company-slug}/{role-slug}/tailored-resume.tex
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
  "Prevented duplicate-signup failures by handling failed API responses and
  re-routing existing profiles to the subscribe flow in NestJS."
- Never write plain "Built X using Y" activity bullets. If the master profile
  phrases something that way, reframe it around the problem it solved or the
  outcome it enabled.
- **Every bullet must contain at least one concrete number** (metric, scale,
  count, duration, accuracy) taken from `resume.md` — 90%, 3,000+, 15 lots,
  100 users, 500K documents, 12-person team, 10+ endpoints, under 3 minutes.
  This is a hard requirement, not a preference:
  - When choosing between candidate facts for a bullet slot, the fact with a
    number wins.
  - Before finishing each role, audit its bullets: at most ONE bullet per
    role may lack a number, and only when `resume.md` genuinely has no number
    for any phrasing of that fact.
  - ONLY numbers that exist in `resume.md`. Never invent or extrapolate.
- When no metric exists after that audit, the result clause is qualitative
  but concrete (what became possible, what failure stopped happening).

## Audience rule — ATS first, recruiter second, engineer last

The resume has two gatekeepers before any engineer reads it: the ATS keyword
scan, then a recruiter skimming for ~7 seconds. Write for them.

- **Hard cap: 25 words per bullet.** Count the words; 26+ is a violation —
  rewrite until it fits. One idea per bullet. No chained arrows (`A → B → C`),
  no multi-clause pile-ups.
- **F-scan rule: the first 3-4 words of every bullet must carry the outcome.**
  Recruiters scan the left edge of the page; a bullet earns its read in its
  opening words ("Cut release cycles to 3 minutes...", "Reached 90% pricing
  accuracy..."). Never open with process framing.
- **No enumeration bullets.** "Shipped X end to end: schema, mutation, queue
  logic" lists the process, not the result — banned. State what the feature
  achieved or enabled; the components stay in the master profile for
  interviews.
- **No parenthetical tech-stack dumps in bullets.** Stack lives on the
  `*Stack:*` line under each role heading (see
  `references/markdown-resume-structure.md`); a bullet names at most 1-2
  technologies, woven into the sentence.
- **Don't re-list the stack line inside bullets.** If the stack line already
  says NestJS, GraphQL, TypeORM, Bull queue, a bullet that recites three of
  them ("by building a NestJS GraphQL API, TypeORM entity, and Bull queue
  job") is redundant noise. Name a technology in a bullet only when that
  specific pairing adds information the stack line can't carry.
- **No low-signal keywords.** Never surface junior/weak-signal work in a
  bullet: "CSS fixes", "styling tweaks", "attended standups", "updated
  documentation". These exist in the master profile for completeness, not for
  the resume. Exception: the JD itself emphasizes that exact skill.
- **One fact, one bullet.** A metric or fact from `resume.md` (e.g. "10-12
  Jiras") may appear in at most ONE bullet per resume. Duplicating a fact
  wastes a slot.
- **Bullet order within each role: Wow → Bridge → ATS.**
  1. *Wow* — the most impressive, metric-backed thing done there. The single
     bullet you'd keep if only one survived.
  2. *Bridge* — the fact that most directly maps this role's work onto the
     JD's requirements, phrased in the JD's language.
  3. *ATS* — the keyword carrier: JD-matching tools, duties, and practices
     woven into one honest bullet.
  The JD decides which fact is Wow vs Bridge — for an AI-heavy JD the GenAI
  tool leads; for a platform JD the production feature might.
- **Self-check before writing files:** re-read every bullet against the
  banned lists (weak starts, clichés, banned verbs, low-signal keywords) and
  the rules above. Fix violations, then write.
- **JD keywords must appear in plain sight** — name the technology the way
  the JD names it (e.g. "CI/CD pipeline", "REST APIs", "PostgreSQL"), because
  that is what the ATS matches on.
- **No implementation internals**: never include function names, file names,
  class names, config values, shell commands, code syntax, or backticked
  identifiers in `tailored-resume.md`. "Automated deployment with a CI/CD
  pipeline (GitHub Actions, AWS EC2)" — not the build → SCP → systemd chain.
- **Plain-English verbs a non-engineer understands**: built, launched,
  automated, reduced, sped up, secured, scaled. The recruiter must grasp what
  happened without knowing what systemd or a Bull queue is.
- **Simple verbs, technical nouns.** Verbs carry zero ATS keyword value, so
  keep them plain — never "orchestrated", "leveraged", "spearheaded",
  "architected", "utilized", "facilitated". The technical precision lives in
  the nouns, which are exactly what the ATS matches: "GraphQL API",
  "PostgreSQL", "RAG pipeline", "CI/CD". A recruiter must follow the sentence;
  an engineer must respect the nouns. Both, always.
- **A project's first bullet must say what the product does for its user**
  before any bullet goes deep on tech — "Built an AI styling app that
  suggests outfits from photos of the user's own wardrobe, powered by OpenAI
  vision models and vector search." If the reader can't tell what the project
  is, the technical bullets after it are wasted.
- Depth lives in the master profile and comes out in interviews — the bullet
  only has to earn the phone screen.

## Tailoring approach

- **Reorder and emphasize, don't invent.** Move the most relevant experience
  and bullets to the top. Trim bullets that are irrelevant to this posting.
- **Keyword alignment.** Where the posting and the resume describe the same
  thing with different words, adopt the posting's phrasing — only when it is
  honestly equivalent (e.g. "CI/CD pipelines" for existing deploy-tooling
  work). Never adopt a keyword for something the candidate hasn't done.
  Full rules in `references/keyword-alignment.md`.
- **Summary rewrite.** Rewrite the summary section to speak to this role,
  using only facts from `resume.md`. Rules:
  - Exactly 3 sentences, ~45-55 words total.
  - **No numbers or metrics in the summary** — accuracy percentages, user
    counts, item counts all live in bullets, never here.
  - Sentence shape: (1) who + degree status + core languages, (2) what has
    been shipped, in plain terms, (3) breadth — ownership across design,
    deployment, APIs, databases, CI/CD.
  - Degree status must match `resume.md` exactly — if it says completed,
    never write "completing", "pursuing", or "expected".
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
