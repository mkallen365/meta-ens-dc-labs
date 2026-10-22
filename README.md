# Meta ENS — Data Center Fabric Labs

Hands-on lab portfolio built during a three-week study sprint (Oct 21 – Nov 10, 2026) preparing for Meta's **Network Engineer, Deployment & Support** role in **Edge & Network Services (ENS)** — data center deployment focus.

## What this is

Leaf-spine (Clos) data center fabrics, built and deliberately broken: deployment lifecycle, fabric routing (eBGP / IS-IS), physical-layer fundamentals, and the automation habits used to deploy and operate networks at scale.

## Lab environment

- Apple Silicon MacBook (M5) running an OrbStack Ubuntu VM (`clab`)
- [Containerlab](https://containerlab.dev) orchestrating containerized network OS images
- FRRouting 10.1.2 nodes (leaf/spine); per-node FRR config files are bind-mounted into the topology so every redeploy comes up with the right daemons already running

## Labs

| Lab | Focus | Status |
| --- | --- | --- |
| Day 1 fabric | 4-node leaf-spine bring-up (leaf1/leaf2/spine1/spine2); FRR daemon setup (`bgpd`/`isisd`/`staticd`) baked into the topology via bind mounts | Done |
| bgp01 | Two-router eBGP (AS 65001 ↔ AS 65002), loopback advertisement, break-fix drill (shutdown neighbor, watch session/prefixes/ping fail, restore) | Done |
| [Day 2 — eBGP fabric](labs/day02-ebgp-fabric/) | eBGP across the fabric: shared spine AS 65000, leaf ASes 65101/65102, loopback + server-subnet advertisement, ECMP | Done |
| Day 3 | BGP troubleshooting — deliberately breaking the fabric, including RFC 8212 (`ebgp-requires-policy`) behavior | Next |

## Themes across the sprint

- Meta DC fabric architecture: Clos/spine-leaf, planes and pods, Wedge / Minipack / FBOSS
- Fabric routing: eBGP (RFC 7938 style) and IS-IS; failure domains and blast radius (capacity vs. reachability)
- Fiber, optics, and physical-layer deployment
- Deployment automation (Python/Linux), vendor and on-site operations

## Layout

- `labs/` — one folder per lab: topology file, node configs, and a README with the goal, addressing plan, and verification output
- `notes/` — concept checks and interview-style Q&A from each study day
