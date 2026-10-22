# Labs

One folder per lab. Each contains the Containerlab topology (`*.clab.yml`), the node configs it mounts, and a README capturing the goal, the addressing/AS plan, and the verification commands with their output.

Deploy any lab from inside the `clab` VM:

```bash
sudo containerlab deploy -t <lab>.clab.yml
docker exec clab-<lab>-leaf1 vtysh -c 'show daemons'
```

FRR note: node daemons (`bgpd`, `isisd`, `staticd`) are enabled by bind-mounting a prepared `daemons` file from the topology — never restart FRR inside a live container, as a restart recreates the container's network namespace and the Containerlab veth links do not survive it.
