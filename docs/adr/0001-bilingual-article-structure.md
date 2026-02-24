# ADR 0001: Bilingual article structure and repository standards

- Status: Accepted
- Date: 2026-02-24

## Context

Nimibyte Academy aims to maximize reach across technical audiences. The repository started with a single article and no formal content governance.

To scale publication quality and consistency, we need:

- A bilingual publishing strategy.
- A stable article folder structure.
- Shared writing rules.
- A place to track repository decisions over time.

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

## Consequences

### Positive

- Wider audience reach with two language versions.
- Predictable navigation for readers and contributors.
- Clear governance for writing style and repository evolution.

### Trade-offs

- Higher maintenance effort because each article has two versions.
- Review process must validate language parity.

## Follow-up

- Add a lightweight publication checklist for EN/ES parity.
- Add new ADRs when structure or editorial policy changes.
