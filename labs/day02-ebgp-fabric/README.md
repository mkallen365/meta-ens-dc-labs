# Day 2 — eBGP in the leaf-spine fabric

Goal: run eBGP across the Day 1 fabric (leaf1, leaf2, spine1, spine2) instead of an IGP.

## Design

- Spines share **AS 65000**; leaf1 = **AS 65101**, leaf2 = **AS 65102**
- Links: 10.0.1.0/30 – 10.0.4.0/30
- Advertised: node loopbacks (10.10.10.x/32) and fake server subnets (172.16.x.0/24)

The shared spine AS is deliberate. There is no spine↔spine peering; with both spines in AS 65000, AS_PATH loop prevention itself kills any leaf→spine→leaf→spine transit path — the RFC 7938 pattern.

## Result

On leaf1, both spine neighbors reached **Established** with 3 prefixes received from each. Leaf1's table shows leaf2's loopback (10.10.10.2/32) and server subnet (172.16.2.0/24) with two paths each (via AS 65000 65102), plus both spine loopbacks — ECMP across the spines working as designed.

## Gotcha worth remembering

A plain ping to a remote loopback fails 100% even when routing is correct: the fabric advertises loopbacks and server nets, not the link /30s, so an echo sourced from a link IP has no return route. Source the ping from the loopback (`ping -I 10.10.10.1 10.10.10.2`) and it passes.

## Policy note

`bgp ebgp-requires-policy` is disabled in this lab. Under RFC 8212 defaults, the sessions would still come up Established but exchange **zero** prefixes until explicit import/export policy exists — which is exactly what production requires. Day 3 turns it back on to watch that happen.
