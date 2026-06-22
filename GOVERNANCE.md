# Astro-Mine Governance

Astro-Mine aims to be **neutral infrastructure** for a field that does not yet have a
standard. Its governance is designed around that goal: a small, jealously-guarded core, a
transparent decision process, and a permissive license that invites commercial use so the
companies that build on the commons help sustain it.

## Principles

1. **Thin core, thick edges.** `Astro-Mine-Core` (the Swarm Asset Description Format, the
   environment and policy/planner APIs, and the message schemas) is the "narrow waist."
   It is small, stable, and slow-changing. Everything valuable lives in plugins.
2. **Contribute once, use everywhere.** A new world, robot, planner, or ISRU process is
   contributed against the Core interfaces and becomes usable in design, training,
   operations, and benchmarks alike.
3. **Open and honest about dual use.** The scientific, simulation, and coordination commons
   is open; genuinely sensitive operational capabilities are partitioned. See
   [`EXPORT_CONTROL.md`](EXPORT_CONTROL.md).

## Roles

- **Contributors** — anyone who opens an issue, PR, or RFC.
- **Maintainers** — review and merge within a package; nominated by existing maintainers
  on a track record of quality contributions.
- **Steering group** — cross-project decisions, the roadmap, and changes to `Core`. Acts
  by rough consensus; the group's composition is published as the project grows.

> During incubation (Phase 0) the steering group is the founding team. As anchor labs and
> contributors join, roles and membership are formalized publicly.

## The RFC process

Substantial changes — anything touching `Core`, a new top-level package, a breaking
interface change, or a cross-cutting convention — go through a lightweight RFC:

1. **Draft.** Open a PR against the [`astro-mine/docs`](https://github.com/astro-mine/docs)
   repository adding `rfc/NNNN-short-title.md` (copy
   [`rfc/0000-template.md`](https://github.com/astro-mine/docs/blob/main/rfc/0000-template.md)).
   Describe the motivation, the design, alternatives considered, and the impact on `Core`.
2. **Discuss.** The PR is the discussion thread. Maintainers and the community comment.
   Minimum comment window: **one week** for Core-affecting RFCs.
3. **Decide.** The steering group (Core RFCs) or package maintainers (package-local RFCs)
   accept, request changes, or decline, with the rationale recorded in the PR.
4. **Track.** Accepted RFCs are merged and their implementation tracked as issues.

Small, non-breaking changes do **not** need an RFC — open a normal PR.

## Decision-making

Day-to-day changes are made by maintainer review and merge. Disagreements escalate to the
steering group, which decides by rough consensus. We optimize for keeping `Core` small:
when in doubt, a capability belongs in a plugin, not the core.

## Licensing

All projects are licensed under **Apache-2.0**. Contributions are accepted under the same
license (inbound = outbound). Permissive licensing is deliberate: it lets companies build
proprietary layers on top, which is precisely what sustains the commons.

## Amending this document

Changes to governance itself follow the RFC process and require steering-group approval.
