# Astro-Mine

**Open-source commons for designing, simulating, and operating planetary robotic swarms for exploration and in-situ resource utilization (ISRU).**

Astro-Mine is a platform for designing, simulating, and ultimately operating large
heterogeneous robotic swarms — orbiters, landers, rovers, hoppers, excavators, haulers,
and ISRU plants — for exploration and resource utilization on the Moon, Mars, and small
bodies. The goal is not a single application but a *commons*: the shared simulation,
benchmark, and orchestration substrate that planetary-swarm robotics is built on — the way
ROS and Gazebo became the substrate for terrestrial robotics and Gymnasium became the
substrate for reinforcement learning.

> **Status:** Phase 1 (autonomy & studio) shipped — the commons seed, the autonomy stack, the
> single console, and the anchor benchmark all run. Phase 2 (operations bridge) is next.
> Repositories are private while we scaffold the commons; they go public at the first public
> benchmark milestone.

## Two modes over one core

- **Design** — specify a goal (*"produce 10 tonnes of water per month from this crater"*)
  and explore swarm compositions, orbital infrastructure, and cooperative policies in
  high-fidelity simulation.
- **Operate** — run a validated campaign, first as a digital-twin shadow of reality and
  eventually commanding real assets through a hardware abstraction layer.

The architecture is a **thin, stable core with thick, swappable edges**: `Core` is small
and changes slowly; worlds, robots, planners, policies, and ISRU processes are all plugins.

## Package map

| Layer | Packages |
|---|---|
| World & environment | `Worlds` · `Prospect` · `Link` |
| Assets | `Fleet` (Swarm Asset Description Format) |
| Simulation | `Sim` · `Surrogate` |
| Autonomy & coordination | `Mind` · `Learn` · `Allocate` · `Guard` |
| Design & operations | `Studio` · `Console` · `View` · `Ops` † · `Bridge` † |
| Commons backbone | `Core` · `Spice` · `Seal` · `Bench` · `Hub` · `Cloud` · `Cli` |

† Phase 2. `Spice` (frames/time/geometry) and `Seal` (signing, SLSA, SBOM) are **Core
companions** — the heavy, shared realizations of Core vocabulary that Core itself stays free
of ([RFC-0002](https://github.com/astro-mine/docs/blob/main/rfc/0002-shared-spice-foundation.md),
[RFC-0005](https://github.com/astro-mine/docs/blob/main/rfc/0005-seal-supply-chain-companion.md)).
`Console` is the single GUI shell every component contributes a surface to
([RFC-0010](https://github.com/astro-mine/docs/blob/main/rfc/0010-console-surface-contract.md));
`Cli` is the `astro-mine <verb>` umbrella
([RFC-0011](https://github.com/astro-mine/docs/blob/main/rfc/0011-umbrella-cli.md)).

## Roadmap

- **Phase 0 — Commons seed** ✅ (`Core`, `Spice`, `Sim`, `Worlds`, `Fleet`, `Bench`, `Prospect`,
  `Link`, `Cloud`) with an anchor scenario: **lunar polar water-ice prospecting**.
- **Phase 1 — Autonomy & studio** ✅ (`Mind`, `Learn`, `Allocate`, `Guard`, `Studio`, `Hub`,
  `Surrogate`, `Seal`, `View`, `Console`, `Cli`).
- **Phase 2 — Operations bridge** (`Ops`, `Bridge`, and the full operations viewer) validated on
  terrestrial analogs.
- **Phase 3 — Flight & ecosystem** — flight-software integration, the multi-regime mission track
  (`Transit`, `Trajectory`, `Sizing`, `Ledger`), and new worlds as plugins.

## Get involved

- 📖 [User guide](https://github.com/astro-mine/docs/blob/main/guide/README.md) — start at
  [getting started](https://github.com/astro-mine/docs/blob/main/guide/getting-started.md)
- 📜 [Governance & RFC process](https://github.com/astro-mine/.github/blob/main/GOVERNANCE.md)
- 🤝 [Contributing guide](https://github.com/astro-mine/.github/blob/main/CONTRIBUTING.md)
- 🛡️ [Security policy](https://github.com/astro-mine/.github/blob/main/SECURITY.md)
- 🌐 [Export-control & dual-use notice](https://github.com/astro-mine/.github/blob/main/EXPORT_CONTROL.md)

Licensed under **Apache-2.0** — permissive by design, so that commercial layers built on
top can fund and sustain the commons.
