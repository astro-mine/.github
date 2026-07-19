# Contributing to Astro-Mine

Thanks for your interest in building the planetary-swarm commons. This guide applies to
every repository in the [`astro-mine`](https://github.com/astro-mine) organization.

## Ways to contribute

- **Plugins** — new worlds, robots, sensors, planners, policies, or ISRU processes written
  against the `Astro-Mine-Core` interfaces. This is the primary way the platform grows:
  *"support a new environment" should mean writing a package, never patching the core.*
  See [**Write a plugin**](https://github.com/astro-mine/docs/blob/main/guide/how-to/write-a-plugin.md)
  for a recipe per extension surface.
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
   the core ([which surface, and when it is an RFC
   instead](https://github.com/astro-mine/docs/blob/main/guide/how-to/write-a-plugin.md#which-surface-do-i-want)).
3. Add tests and update docs.
4. Run the repo's linters and test suite locally (see each repo's `README`). Cover the code
   you add — CI enforces a coverage gate (see [Testing & coverage](#testing--coverage)).
5. Open a pull request using the template. Link the issue/RFC it addresses.

## Testing & coverage

Every repository enforces a **95% overall test-coverage gate** in CI: a change that pushes
coverage below 95% fails the build. Cover the code you add. If a line genuinely cannot be
tested, exclude it explicitly (see below) rather than lowering the bar.

The gate is wired the same way in every Python repo so it behaves identically everywhere:

- **CI step** (`.github/workflows/ci.yml`) — run the suite under coverage and fail under 95%:

  ```yaml
  - name: Test (pytest + coverage gate)
    run: uv run pytest --cov --cov-report=term-missing --cov-fail-under=95
  ```

  Keep `--cov-fail-under` in the CI invocation (not in `addopts`) so that running a single
  test file locally doesn't fail spuriously on partial coverage.

- **`pyproject.toml`** — add `pytest-cov` to the dev dependency group, then configure coverage
  so the gate measures *implemented* code: generated bindings are omitted, and
  not-yet-implemented placeholders, type-only, and protocol-interface lines are excluded (a
  stub that later gains a real body must then be tested). Adjust `source` to the package name:

  ```toml
  [tool.coverage.run]
  source = ["src/<package>"]
  omit = ["*/_proto/*"]            # generated protobuf bindings, not hand-maintained

  [tool.coverage.report]
  show_missing = true
  exclude_also = [
    "if TYPE_CHECKING:",
    "raise NotImplementedError",   # not-yet-implemented placeholders
    "^\\s*\\.\\.\\.$",             # protocol-interface / stub bodies
    "@(typing\\.)?overload",
  ]
  ```

New component repos should copy this block so they inherit the gate from day one.

## Pull request expectations

- One logical change per PR; keep them reviewable.
- All CI checks green, including the [95% coverage gate](#testing--coverage). CI runs with
  read-only token permissions by default.
- A maintainer reviews and merges. Be responsive to review feedback.

## Commit & license terms

By contributing you agree your work is licensed under **Apache-2.0** (inbound = outbound),
the same license as the project. Do not contribute code you do not have the right to
license this way.

## Code of conduct

All participation is governed by our [Code of Conduct](CODE_OF_CONDUCT.md).
