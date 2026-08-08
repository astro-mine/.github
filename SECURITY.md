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

## Signing keys and the trust root

Artifacts are signed (Sigstore/cosign) and verified at admission and at pull. *Whose* signature
counts is the **trust root**: a set of named signers, each with an optional validity window and an
optional artifact-kind scope. The rule is normative in
[`conventions.md` §9](https://github.com/astro-mine/docs/blob/main/architecture/conventions.md);
this section is the procedure.

**The root is a set, and that is what makes rotation safe.** With a single trusted key there is an
instant at which every previously signed artifact stops verifying, so a rollover is a flag day
across every consumer at once. With a set, the successor and the predecessor are both honoured for
an overlap window and nothing breaks at any moment.

### Rotating a signing key

1. **Mint** the successor (`astro-mine hub keygen`) and store the private key where the current one
   lives. Never in a repository, an image, or an issue.
2. **Publish** a trust root containing *both* keys: the predecessor with a `not_after` at the end of
   the overlap, the successor with a `not_before` of now. Ship it as
   `src/astro_mine/seal/trust_root.json` and cut a release, or distribute it out of band via
   `$ASTRO_MINE_TRUST_ROOT` for a deployment that cannot wait for one.
3. **Wait out the overlap.** It must be at least as long as the slowest consumer's upgrade cycle —
   anyone still on the old root has to have picked up the new one *before* the predecessor expires,
   or their pulls start failing.
4. **Sign new artifacts with the successor** from step 2 onward. Artifacts already signed by the
   predecessor keep verifying until it expires; they do **not** need re-signing, because a signature
   is over content that has not changed.
5. **Remove the predecessor** from the root after its `not_after`, and cut a release.

Choosing `not_after` in step 2 rather than remembering step 5 is the point of the window: the
retirement is scheduled when the rotation is planned, not deferred to somebody's calendar.

### Revoking a key

Revocation is **removal from the root plus a release**, and it is intentionally not a separate
mechanism: a key that is no longer in the set is not trusted, at every gate, with no extra state to
distribute or check.

Removal is retroactive — every artifact that key ever signed stops verifying. That is correct for a
compromise and wrong for an ordinary retirement, so use a scheduled `not_after` for the latter. If
artifacts signed by a compromised key must remain available, they have to be **re-signed** by a
trusted key and re-published; there is no way to trust a signature and distrust its signer.

Report a suspected key compromise through the process at the top of this file. Do not open a public
issue.

### What is not yet enforced

The packaged trust root is **empty**, which means it can never be the reason an artifact is
accepted, and `require_signature` is `False` outside the hosted tier. Enforcement posture — flipping
it on for the hosted tier and Guard's load gate — is tracked in
[`astro-mine-platform#22`](https://github.com/astro-mine/astro-mine-platform/issues/22). Until then,
signature *identity* is checked only where a caller passes a root.
