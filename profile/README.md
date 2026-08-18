# Astro-Mine

**Open-source commons for designing, simulating, and operating planetary robotic swarms for exploration and in-situ resource utilization (ISRU).**

Astro-Mine is a platform for designing, simulating, and ultimately operating large
heterogeneous robotic swarms — orbiters, landers, rovers, hoppers, excavators, haulers,
and ISRU plants — for exploration and resource utilization on the Moon, Mars, and small
bodies. The goal is not a single application but a *commons*: the shared simulation,
benchmark, and orchestration substrate that planetary-swarm robotics is built on — the way
ROS and Gazebo became the substrate for terrestrial robotics and Gymnasium became the
substrate for reinforcement learning.

> **Status:** Phases 0 and 1 shipped — the commons seed, the autonomy stack, the console, and the
> anchor benchmark all run. Phase 2 (operations bridge) is next.
>
> The code is public; **the distributions are not yet published to a package index**, so you install
> from source for now (`VERSIONING.md` §6.2). Nothing here is a released, supported artifact yet —
> distributions are `0.y` and interfaces can still move.

## Two modes over one core

- **Design** — specify a goal (*"produce 10 tonnes of water per month from this crater"*)
  and explore swarm compositions, orbital infrastructure, and cooperative policies in
  high-fidelity simulation.
- **Operate** — run a validated campaign, first as a digital-twin shadow of reality and
  eventually commanding real assets through a hardware abstraction layer.

The architecture is a **thin, stable core with thick, swappable edges**: `Core` is small
and changes slowly; worlds, robots, planners, policies, and ISRU processes are all plugins.

## What ships

**A component is a unit of design; a distribution is a unit of release.** Four things ship, and
every component is imported as `astro_mine.<name>` from the first of them:

| Distribution | What it is |
|---|---|
| [`astro-mine-platform`](https://github.com/astro-mine/astro-mine-platform) | Every component, one Python wheel. A library — no server, no front end. |
| [`astro-mine-cli`](https://github.com/astro-mine/astro-mine-cli) | The one executable: `astro-mine <component> <verb>`. |
| [`astro-mine-api`](https://github.com/astro-mine/astro-mine-api) | The REST tier — Hub, Studio, Cloud and Bench surfaces. |
| [`astro-mine-ui`](https://github.com/astro-mine/astro-mine-ui) | The console: one Next.js application over four libraries. |

## Component map

| Layer | Components |
|---|---|
| World & environment | `Worlds` · `Prospect` · `Link` |
| Assets | `Fleet` (Swarm Asset Description Format) |
| Simulation | `Sim` · `Surrogate` |
| Autonomy & coordination | `Mind` · `Learn` · `Allocate` · `Guard` |
| Design & operations | `Studio` · `View` · `Ops` † · `Bridge` † |
| Commons backbone | `Core` · `Spice` · `Seal` · `Bench` · `Hub` · `Cloud` |

† Phase 2. [`Spice`](https://github.com/astro-mine/docs/blob/main/architecture/spice.md)
(frames/time/geometry) and
[`Seal`](https://github.com/astro-mine/docs/blob/main/architecture/seal.md) (signing, SLSA,
SBOM) are **Core companions** — the heavy, shared realizations of Core vocabulary that Core
itself stays free of.
The **console** is not a component: it is the single GUI, and it is the `astro-mine-ui`
application itself — adding a page is adding a route
([`ui.md`](https://github.com/astro-mine/docs/blob/main/architecture/ui.md)). `View` survives as
the `@astro-mine/view` visualization library.

## Roadmap

- **Phase 0 — Commons seed** ✅ (`Core`, `Spice`, `Sim`, `Worlds`, `Fleet`, `Bench`, `Prospect`,
  `Link`, `Cloud`) with an anchor scenario: **lunar polar water-ice prospecting**.
- **Phase 1 — Autonomy & studio** ✅ (`Mind`, `Learn`, `Allocate`, `Guard`, `Studio`, `Hub`,
  `Surrogate`, `Seal`, `View`), followed by the packaging consolidation into the four
  distributions above.
- **Phase 2 — Operations bridge** (`Ops`, `Bridge`, and the full operations viewer) validated on
  terrestrial analogs.
- **Phase 3 — Flight & ecosystem** — flight-software integration, the multi-regime mission track
  (`Transit`, `Trajectory`, `Sizing`, `Ledger`), and new worlds as plugins.

## Get involved

- 📖 [User guide](https://github.com/astro-mine/docs/blob/main/guide/README.md) — start at
  [getting started](https://github.com/astro-mine/docs/blob/main/guide/getting-started.md)
- 📜 [Governance](https://github.com/astro-mine/.github/blob/main/GOVERNANCE.md) — how changes
  are governed, and what a change to `Core` has to clear
- 🤝 [Contributing guide](https://github.com/astro-mine/.github/blob/main/CONTRIBUTING.md)
- 🛡️ [Security policy](https://github.com/astro-mine/.github/blob/main/SECURITY.md)
- 🌐 [Export-control & dual-use notice](https://github.com/astro-mine/.github/blob/main/EXPORT_CONTROL.md)

Licensed under **Apache-2.0** — permissive by design, so that commercial layers built on
top can fund and sustain the commons.
