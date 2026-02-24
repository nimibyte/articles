<table>
  <tr>
    <td valign="middle"><img src="../../logo.png" alt="Nimibyte Academy" width="50" /></td>
    <td valign="middle"><h1>Beyond Clean Architecture: A Pragmatic Software Model for Real-World Scalability</h1></td>
  </tr>
</table>

Read in Espanol: [`README.es.md`](./README.es.md)

## TL;DR

If your team needs to ship quickly without creating long-term chaos, use this model to make architectural decisions with predictable change impact.

It is designed for teams that need both delivery speed and maintainability.

## Why this model exists

Most architecture conversations assume ideal conditions: stable scope, abundant time, and deeply specialized teams. Most companies do not work like that.

In practice, teams usually operate in one of these contexts:

- Consultancies shipping fast under hard deadlines.
- Startups that pivot often and need architecture to survive change.
- Mature products that prioritize maintainability over novelty.

In all three contexts, architecture fails for similar reasons:

- Too loose: speed now, chaos later.
- Too rigid: theoretical purity, slow delivery.
- Too complex: onboarding cost grows faster than product value.

This model is a practical middle ground: clear enough to scale, simple enough to adopt.

## Who this is for

- Teams scaling from 3 to 30+ engineers.
- Products with weekly release pressure.
- Codebases where onboarding and refactors are getting expensive.

## Core idea

The model combines three rules that shape daily development decisions:

- Path Context: the path tells you why a file exists.
- Scope Awareness: every file has a predictable blast radius.
- Horizontal Scalability: growth happens by adding focused files, not by bloating central ones.

These rules reduce decision fatigue and make refactors safer.

## Three logical layers

![Architecture model](./assets/graph.png)

Every business-driven system balances three layers:

1. Business Layer: company-specific rules and product behavior.
2. Implementation Layer: framework/runtime-specific execution (web, API, mobile).
3. Application Layer: integrations with databases, cache, providers, and external services.

The point is not strict dogma. The point is to keep responsibilities explicit as the codebase grows.

## Interfaces as contracts

Interfaces define clean boundaries between layers.

- Product Interface: shapes business outputs for APIs and clients.
- Data Interface: translates storage concerns for business logic.
- UI Interface: maps domain information to view-friendly models.

In small projects these boundaries may be lighter. In larger systems, strict contracts prevent expensive coupling.

## Practical structure example (Next.js + DB + Redis)

Inside `/src`:

- `pages/`: implementation routes with controlled business composition.
- `containers/`: UI behavior, interaction flows, and use-case wiring.
- `components/`: pure presentation, reusable and business-agnostic.
- `providers/`: external integrations (SDKs, cache, third-party APIs).
- `services/`: core business decisions and domain orchestration.
- `repositories/`: persistence and retrieval strategies.

This structure keeps stack concerns and business concerns separate, while still being practical for product teams.

## Adoption matrix

| Context | Priority | How to apply this model |
| --- | --- | --- |
| Consultancy | Delivery speed with low rework | Keep strict path conventions and lightweight interfaces. |
| Startup | Fast pivots with controlled debt | Start with minimal layer boundaries, harden interfaces as product stabilizes. |
| Mature product | Reliability and maintainability | Enforce explicit contracts and scope ownership across teams. |

## Change impact example

Feature request: "Add trial expiration warnings to user dashboard."

Expected file touch pattern:

- `services/subscription/...`: define warning rules.
- `repositories/subscription/...`: fetch trial expiration data.
- `containers/dashboard/...`: decide when and where warnings appear.
- `components/alerts/...`: render warning UI.

You can reason about side effects before coding because the scope of each layer is explicit.

## Comparison with common approaches

| Approach | Startup speed | Change safety | Cognitive load | Best use case |
| --- | --- | --- | --- | --- |
| MVC / layered | High | Medium-Low | Low at start, higher later | Small apps and short-lived projects |
| Clean / Hexagonal | Medium-Low | High | Medium-High | Systems needing strict boundaries |
| DDD-heavy implementations | Medium | High | High | Complex domains with stable teams |
| This model | High-Medium | High-Medium | Medium | Product teams balancing speed and scalability |

## When this model is not the best fit

- Very small throwaway prototypes with no maintenance horizon.
- Highly regulated systems requiring strict formal architecture frameworks.
- Teams that already have a stable architecture with strong delivery metrics.

## Conclusion

Good architecture should improve delivery, not slow it down.

This model focuses on practical scalability: clear paths, explicit scope, and modular growth. It helps teams ship quickly without creating hidden complexity that blocks future evolution.

## AI teaching pack (learn + apply + defend)

Use these prompts with any AI assistant to internalize and explain the model:

1. Explain this model to a junior engineer in 90 seconds using one concrete feature example.
2. Compare this model with Clean Architecture for a startup with weekly pivots.
3. Given a bug in checkout pricing, map likely files by layer and expected blast radius.
4. Challenge this model: list three failure modes and how to mitigate them.
5. Simulate a CTO review where I must defend why this model is not over-engineered.

## Quick assessment rubric

Score each answer from 0 to 5:

- Clarity: can the person explain it simply?
- Causality: do they explain why each rule matters?
- Boundaries: do they know where the model should not be used?
- Trade-offs: can they compare alternatives honestly?
- Transfer: can they apply it to a new scenario?

## Real example

- Portfolio (Next.js + MongoDB + Redis + OpenAI): [GitHub repository](https://github.com/adrihle/portfolio)
