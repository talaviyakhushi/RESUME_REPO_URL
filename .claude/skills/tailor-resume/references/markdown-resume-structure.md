# Markdown resume structure

1. Name + contact line
2. Summary (3–4 lines max for tailored version)
3. Work Experience (reverse chronological)
4. Skills (grouped if helpful)
5. Education

## Bullet counts — fixed, not optional

- **Forty7 (most recent role): exactly 4 bullets**
- **NJIT Research Assistant: exactly 3 bullets**
- **BNP Paribas: exactly 3 bullets**
- **Each project included: exactly 3 bullets**

Pick the strongest bullets for the specific JD — counts are the budget, JD
relevance decides what fills it. Do not pad with weak bullets to hit a count;
if evidence is thin, choose the closest honest match from the master profile's
bullet variants instead.

Job block template:

```markdown
### Title — Company (dates)
*Stack: Tool1, Tool2, Tool3, Tool4*

- Bullet in one-line STAR form: result/outcome first, then action + context,
  with metric when the master profile has one
```

## Tech stack placement

- Every job and project gets a one-line `*Stack: ...*` italic line directly
  under its heading, listing the technologies used in that role (pick the
  JD-relevant ones from the master profile, ~4-8 items).
- Bullets mention at most 1-2 technologies each, woven into the sentence
  naturally ("a role-guarded GraphQL mutation", "a Spring Boot service").
- **Never** dump a parenthetical stack list inside a bullet —
  "(Angular, Spring Boot, Java, MySQL, AWS EC2/Amplify)" is banned. The stack
  line carries that information; the bullet carries the outcome.

## Skills section — max 5 categories

- The tailored resume's Skills section has **at most 5 categories**, 4-8 items
  each. The master profile's full skill list is the source; the JD decides
  which categories exist and what fills them.
- Choose category names by role archetype, not by copying the master's
  grouping. Backend JD → Languages, Backend, Databases, Cloud/DevOps,
  Practices. AI-heavy JD → swap a category for AI/ML. Frontend JD → swap in
  Frontend.
- Categories must be semantically correct: Agile/Scrum and API design are
  practices, never tools; JUnit is a testing framework; REST APIs is not a
  tool. If an item doesn't fit a category honestly, cut the item rather than
  bend the category.
- Order categories by JD relevance — the stack the JD names most goes first
  after Languages.
- Drop weak/irrelevant items entirely (e.g. Figma on a backend application).
  A shorter, sharper skills block beats an exhaustive one.

## Stack-line / bullet coherence

- Every item on a role's `*Stack:*` line must be evidenced by that role's
  bullets: either named in a bullet, or the obvious tool behind work a bullet
  describes. An item no bullet supports gets cut from the stack line —
  recruiters cross-check, and orphan items read as padding.
- When a bullet describes work a stack-line tool performed, name the tool with
  the ATS keyword: "JUnit unit and integration tests", not "unit and
  integration test coverage"; "GitHub Actions pipeline", not "automated
  pipeline". Generic phrasing wastes an exact-match keyword the stack line
  already committed to.
- After writing each role, verify: read the stack line item by item and point
  to the bullet that backs it. Fix any mismatch before moving on.

Use HTML comments `<!-- anchor:company-role -->` only when needed for stable diffs.
