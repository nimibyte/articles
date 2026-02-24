# ADR 0001: Bilingual, AI-first content structure and repository standards

- Status: Accepted
- Date: 2026-02-24

## Context

Nimibyte Academy aims to maximize reach across technical audiences. The repository started with a single article and no formal content governance.

To scale publication quality and consistency, we need:

- A bilingual publishing strategy.
- An AI-first learning approach that works for modern consumption patterns.
- A stable article folder structure.
- Shared writing rules.
- A place to track repository decisions over time.

Most readers now use AI assistants instead of reading long-form content linearly. To remain useful, content must be understandable by both humans and AI systems, and it must support explanation, challenge, and evaluation workflows.

## Decision

1. Every article is published in English and Spanish.
2. Each article folder uses:
   - `README.md` as language selector.
   - `README.en.md` as English version.
   - `README.es.md` as Spanish version.
3. The project uses a global style guide at `docs/style-guide.md`.
4. Repository-level decisions are documented in `docs/adr/`.
5. The project name is standardized as "Nimibyte Academy".
6. The global logo is stored at repository root as `logo.png` and shown in article headers.
7. Content follows an AI-first publishing model:
   - Canonical concept article for human reading (`README.en.md`, `README.es.md`).
   - Structured knowledge artifacts to support AI tutoring and retrieval.
   - Evaluation artifacts to validate understanding, not memorization.
8. Every core topic should evolve toward a "learn + apply + defend" workflow:
   - Learn: concise principles and boundaries.
   - Apply: scenario-based examples and decision paths.
   - Defend: prompts/questions to explain trade-offs and limits.
9. Claims should be practical and testable, with explicit boundaries:
   - Include when to use and when not to use the model.
   - Avoid universal statements without context.
   - Prefer evidence from real implementation patterns.

## Consequences

### Positive

- Wider audience reach with two language versions.
- Better adaptation to AI-driven consumption and learning workflows.
- Predictable navigation for readers and contributors.
- Clear governance for writing style and repository evolution.

### Trade-offs

- Higher maintenance effort because each article has two versions.
- Review process must validate language parity.
- Additional effort to keep canonical articles and AI/evaluation artifacts aligned.

## Follow-up

- Add a lightweight publication checklist for EN/ES parity.
- Add a publication checklist that also validates AI-first artifacts and evaluation quality.
- Add new ADRs when structure or editorial policy changes.
