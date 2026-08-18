# Astro-Mine Governance

Astro-Mine aims to be **neutral infrastructure** for a field that does not yet have a
standard. Its governance is designed around that goal: a small, jealously-guarded core, a
transparent decision process, and a permissive license that invites commercial use so the
companies that build on the commons help sustain it.

## Principles

1. **Thin core, thick edges.** `astro_mine.core` (the Swarm Asset Description Format, the
   environment and policy/planner APIs, and the message schemas) is the "narrow waist."
   It is small, stable, and slow-changing. Everything valuable lives in plugins.
2. **Contribute once, use everywhere.** A new world, robot, planner, or ISRU process is
   contributed against the Core interfaces and becomes usable in design, training,
   operations, and benchmarks alike.
3. **Open and honest about dual use.** The scientific, simulation, and coordination commons
   is open; genuinely sensitive operational capabilities are partitioned. See
   [`EXPORT_CONTROL.md`](EXPORT_CONTROL.md).

## Roles

- **Contributors** — anyone who opens an issue or PR.
- **Maintainers** — review and merge within a package; nominated by existing maintainers
  on a track record of quality contributions.
- **Steering group** — cross-project decisions, the roadmap, and changes to `Core`. Acts
  by rough consensus; the group's composition is published as the project grows.

> During incubation (Phase 0) the steering group is the founding team. As anchor labs and
> contributors join, roles and membership are formalized publicly.

## How changes are governed

**By mechanism, not by ceremony.** The project ran a formal design-proposal process during
incubation and has retired it. Proposals are ordinary issues, changes are ordinary pull
requests, and what protects the narrow waist is machinery that cannot be talked past in
review. A process that cannot fail a bad change is decoration; a check that fails the build
is governance.

**Where a decision is recorded.** A decision lives in the document where it is normative,
not in a parallel archive of proposals that a reader has to reconcile against the docs:

- the [charter](https://github.com/astro-mine/docs/blob/main/charter/Swarm_Exploration_ISRU_Orchestrator_OSS_Project.md)
  for scope and vision;
- [`architecture/conventions.md`](https://github.com/astro-mine/docs/blob/main/architecture/conventions.md)
  for cross-cutting standards that bind every component;
- the owning component's document in
  [`architecture/`](https://github.com/astro-mine/docs/tree/main/architecture) for its own
  contract.

A change to how the platform works is not done until the document that governs it says so.

**What a change to `Core` has to clear.** The narrow waist is guarded by checks, not by a
waiting period. A Core change MUST:

1. **name a consumer** — a contract nobody is asking for is speculation, and the waist stays
   small by refusing it;
2. **be additive** — schema fields are append-only, and a published schema `$id` is public API
   that is never repurposed or removed;
3. **be wire-compatible** — verified mechanically (`buf breaking`), not by reading the diff;
4. **be green against every consumer** — a Core change runs every component's schema and
   contract tests in the same CI run, so a change that breaks a consumer fails the pull
   request that breaks it.

A change that cannot clear all four is a breaking interface change: it needs a new major
interface version and a deprecation window, and it is the steering group's call.
[`architecture/conventions.md`](https://github.com/astro-mine/docs/blob/main/architecture/conventions.md)
§3 and §11 are normative for the details.

Everything else — a plugin, a world, a scenario, a fix, a doc — is an ordinary pull request.
Open an issue first for anything substantial, so the approach can be discussed before the
code is written.

## Decision-making

Day-to-day changes are made by maintainer review and merge. Disagreements escalate to the
steering group, which decides by rough consensus. We optimize for keeping `Core` small:
when in doubt, a capability belongs in a plugin, not the core.

## Licensing

All projects are licensed under **Apache-2.0**. Contributions are accepted under the same
license (inbound = outbound). Permissive licensing is deliberate: it lets companies build
proprietary layers on top, which is precisely what sustains the commons.

## Amending this document

Changes to governance itself land as ordinary pull requests against this repository and
require steering-group approval to merge. The rationale belongs in the pull request, which
is the record of the decision.
