# Resume repository

For job tailoring runs, use the **`tailor-resume`** skill:

- Read `.claude/skills/tailor-resume/SKILL.md` first and follow it exactly
- Treat `resume.md` as the single source of truth for facts
- Write per-job outputs under `jobs/<company-slug>/<role-slug>/`: a short `fit-report.md` (tier, verdict, 1-2 sentence reason) and a ready-to-compile `tailored-resume.tex`
- In `fit-report.md`, include `**Tier:**` and `**Verdict:**` lines

Do not invent experience. Unsupported requirements are silently excluded from the tailored resume, never fabricated.
