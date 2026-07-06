# Recruiter-side heuristics

Rules for maximizing ATS pass rate and recruiter approval. Apply to every
`tailored-resume.md`. (Adapted from career-ops recruiter-side heuristics.)

## Recruiter-side risk map (internal, never printed)

Before writing bullets, map the doubts a recruiter will have and pick content
that closes each one:

| Potential doubt | Evidence to surface | Fix in the resume |
|-----------------|---------------------|-------------------|
| Can they do this stack? | Matching tools, systems, projects | Put the exact JD stack keywords in truthful context |
| Are they senior enough? | Ownership, scope, sole-developer work, tradeoffs | Lead with ownership behaviors, not tenure |
| Is the domain relevant? | Similar users, workflows, scale | Translate adjacent experience into the JD's language |
| Is the application generic? | Weak or broad bullets | Rewrite around this role's concrete problems |

Never invent evidence to close a doubt — an unclosable doubt goes in the fit
report's Gaps section instead.

## Six-second clarity gate

The top third of the resume (summary + first experience bullets) must make fit
impossible to miss. A recruiter reading only that must see:

- target role/archetype matching the JD title
- strongest matching stack or domain
- one production or business outcome (with a real metric when one exists)

If fit must be inferred from scattered bullets lower down, rewrite the summary
and the first bullets until it doesn't.

## Business-value bullet patterns

Prefer: `Action + system/scope + tool + outcome + proof`

- `Resolved [problem] in [system], improving [business/system effect].`
- `Built [capability] with [tools], enabling [user/team outcome].`
- `Migrated [old] to [new], reducing [risk/cost/latency/debt].`
- `Improved [metric] from [before] to [after] by [technical action].`

**Banned weak starts** (when stronger ownership is true): "helped", "assisted",
"responsible for", "worked on", "participated in", "contributed to".

**Banned clichés — never generate these in any output:**

- "passionate about …"
- "results-oriented professional" / "proven track record"
- "leveraged cutting-edge …"
- "spearheaded a strategic initiative"
- "cross-functional synergies"
- "robust, scalable solutions"
- "in today's fast-paced …"
- "demonstrated ability to drive innovative outcomes"

## ATS reality check

Optimize for parseability and honest keyword match, not tricks:

- exact JD keywords, only in truthful context
- no keyword stuffing, hidden text, or white-font tricks
- no skills or metrics not present in `resume.md`

## ASCII normalization — required

ATS parsers choke on typographic Unicode. In `tailored-resume.md` use only
ASCII punctuation:

| Never use | Use instead |
|-----------|-------------|
| em-dash `—` (U+2014) | hyphen `-` |
| en-dash `–` (U+2013) | hyphen `-` (e.g. `2020-2024`, `Jan 2024 - Jul 2024`) |
| curly quotes `" " ' '` | straight `"` and `'` |
| ellipsis `…` | `...` |
| non-breaking / zero-width spaces | regular space |

This applies to `tailored-resume.md` only; the fit report and change summary
may use normal typography.
