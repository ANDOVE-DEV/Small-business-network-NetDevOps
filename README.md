# Small Business Network - NetDevOps Approach

## 🎯 Overview
Design and implementation of a complete network infrastructure for a small business (50 employees), built using Infrastructure as Code (IaC) principles.

## 🏗️ Architecture
- **VLANs:** 5 logical segments (Management_HR, Sales, IT_Servers, Guest_WiFi, Network_Management)
- **IP Schema:** 10.10.0.0/16 with consistent /24 subnets
- **Tools:** Containerlab, FRRouting (FRR), Ansible, Git

## 📋 Prerequisites
- Windows 11 with WSL2
- Docker Desktop (with WSL2 integration enabled)
- Containerlab
- VSCode with WSL extension

## 🚀 Quick Start
To deploy the network topology locally:
```bash
cd lab
sudo containerlab deploy