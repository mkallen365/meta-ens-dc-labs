# Notes

Concept checks from each study day, kept in interview format: the question, my answer, and the graded feedback / model answer.

- **Day 1 — fabric fundamentals:** blast radius and failure domains (a lost plane or spine costs capacity, not reachability); the leaf-spine-leaf path between any two servers in a pod; the on-call view of a spine failure (alarms, BGP session loss, capacity dashboards) vs. the user view (at most reduced throughput).
- **Day 2 — eBGP design:** why eBGP instead of an IGP in the fabric; why the spines share one AS; what `ebgp-requires-policy` (RFC 8212) actually does.
