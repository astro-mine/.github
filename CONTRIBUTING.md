# Contributing to Astro-Mine

Thanks for your interest in building the planetary-swarm commons. This guide applies to
every repository in the [`astro-mine`](https://github.com/astro-mine) organization.

## Ways to contribute

- **Plugins** — new worlds, robots, sensors, planners, policies, or ISRU processes written
  against the `Astro-Mine-Core` interfaces. This is the primary way the platform grows:
  *"support a new environment" should mean writing a package, never patching the core.*
- **Benchmarks & baselines** — new scenarios for `Bench`, or methods that beat the
  leaderboard.
- **Core & infrastructure** — improvements to the simulation engine, the core interfaces,
  or the tooling. Changes to `Core` go through the [RFC process](GOVERNANCE.md#the-rfc-process).
- **Docs, examples, and bug reports** — always welcome.

## Before you start

- For anything substantial, **open an issue first** to discuss the approach. For changes to
  `Core`, a new top-level package, or a breaking interface change, open an **RFC** (see
  [`GOVERNANCE.md`](GOVERNANCE.md)).
- Check that your contribution respects the [export-control & dual-use
  posture](EXPORT_CONTROL.md). When in doubt, ask before writing code.

## Development workflow

1. Fork the repository and create a branch off `main`.
2. Make your change. Keep `Core` interfaces stable — prefer adding a plugin over widening
   the core.
3. Add tests and update docs.
4. Run the repo's linters and test suite locally (see each repo's `README`).
5. Open a pull request using the template. Link the issue/RFC it addresses.

## Pull request expectations

- One logical change per PR; keep them reviewable.
- All CI checks green. CI runs with read-only token permissions by default.
- A maintainer reviews and merges. Be responsive to review feedback.

## Commit & license terms

By contributing you agree your work is licensed under **Apache-2.0** (inbound = outbound),
the same license as the project. Do not contribute code you do not have the right to
license this way.

## Code of conduct

All participation is governed by our [Code of Conduct](CODE_OF_CONDUCT.md).
