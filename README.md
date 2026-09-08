# Small Business Network - NetDevOps Approach

## 🎯 Overview
Design and implementation of a small business network (`technova-network`) built with
Infrastructure as Code (IaC) principles. The whole topology runs in Containerlab: an
FRRouting (FRR) router performs inter-segment routing with OSPF, plain L2 bridges provide
the access layer, and Alpine containers act as clients and access point.

## 🏗️ Architecture
- **Topology:** 1 router (FRR v8.4.1) + 2 L2 bridges (`switch1`, `switch2`) + 1 access
  point (`ap1`) + 3 clients (`client-hr`, `client-sales`, `client-guest`)
- **Inter-switch link:** a plain L2 bridge-to-bridge connection (`switch1:s1p4` ↔
  `switch2:s2p4`), not an 802.1Q trunk
- **Segmentation:** routed at L3 on separate router interfaces — no 802.1Q VLANs, the
  switches are simple broadcast domains (`kind: bridge`)
- **IP Schema:** 10.10.0.0/16 supernet advertised in OSPF, split into /24 subnets:
  - `10.10.10.0/24` — HR + Sales (router `eth1`, gateway `10.10.10.1`, on `switch1`)
  - `10.10.20.0/24` — Guest (router `eth2`, gateway `10.10.20.1`, on `switch2`)
  - `10.10.40.0/24` — WiFi / AP (router `eth3`, gateway `10.10.40.1`)
- **Routing:** OSPF area 0 (`network 10.10.0.0/16 area 0`, router-id `10.10.99.1`)
- **Tools:** Containerlab, FRRouting (FRR/OSPF), Git
- **Automation (WIP):** the `ansible/` folder is currently empty (no playbooks yet);
  Containerlab auto-generates `lab/clab-technova-network/ansible-inventory.yml` at deploy time

## 📋 Prerequisites
Containerlab needs a Linux kernel, so the lab runs on a Linux host or inside WSL2.
- Linux host **or** Windows with WSL2 (Ubuntu)
- Docker Engine — install it with the bundled script: `sudo sh get-docker.sh`
- Containerlab — see https://containerlab.dev/install
- (optional) VSCode with the WSL extension for editing

## 🚀 Quick Start
To deploy the network topology locally:
```bash
cd lab
sudo containerlab deploy -t technova.clab.yaml
```
