# Diagrams (diagrams-as-code)

Editable [Mermaid](https://mermaid.js.org/) sources for the `technova-network` design.
These files mirror the diagrams embedded in [`../design.md`](../design.md) — keep them in
sync when the topology changes.

| File | Shows |
|------|-------|
| `topology.mmd` | L2/physical topology: nodes, links, interfaces, broadcast domain |
| `addressing.mmd` | L3 view: subnets, gateways, host addresses |
| `ospf.mmd` | OSPF configuration on the FRR router |
| `management.mmd` | Containerlab out-of-band management network |

## Rendering

- **VS Code:** install the *Markdown Preview Mermaid Support* or *Mermaid Preview*
  extension and preview the `.mmd` file (or the fenced blocks in `design.md`).
- **GitHub:** the diagrams render automatically inside `design.md` (```` ```mermaid ````
  fenced blocks). Standalone `.mmd` files are not rendered by GitHub.
- **CLI (export to SVG/PNG):**
  ```bash
  npm install -g @mermaid-js/mermaid-cli
  mmdc -i topology.mmd -o topology.svg
  ```
- **Online:** paste the content into <https://mermaid.live>.

> Management IPs in `management.mmd` are auto-assigned by Containerlab at deploy time and
> are **not** part of the IaC source (the runtime dir `lab/clab-technova-network/` is
> git-ignored), so they may change between deployments.
