# Security Policy

This policy applies to all repositories in the [`astro-mine`](https://github.com/astro-mine)
organization.

## Reporting a vulnerability

**Please do not report security vulnerabilities through public issues.**

Instead, use GitHub's **private vulnerability reporting**: on the affected repository, go to
the **Security** tab → **Report a vulnerability**. This opens a private advisory visible
only to maintainers.

Please include:

- the affected repository, package, and version/commit;
- a description of the vulnerability and its impact;
- steps to reproduce, ideally with a minimal proof of concept.

## What to expect

- **Acknowledgement** within a few business days during incubation.
- We will investigate, keep you updated, and coordinate a fix and disclosure timeline with
  you. We aim to credit reporters who wish to be named.

## Scope

Security-relevant issues include, but are not limited to: vulnerabilities in the simulation
or autonomy code, the plugin/registry mechanism, leaked secrets, and dependency
vulnerabilities. Note that Astro-Mine deliberately keeps certification-grade operational
flight-targeting **out of scope** — see [`EXPORT_CONTROL.md`](EXPORT_CONTROL.md).

## Supported versions

During Phase-0 incubation only the latest `main` of each repository is supported. A formal
support matrix will be published once we cut tagged releases.
