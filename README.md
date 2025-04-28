# Hydra Cluster: The VPN-Driven Raspberry Pi + Jetson Nano Kubernetes Empire

Welcome to Project Hydra — a decentralized, air-gapped Kubernetes cluster focused on VPN routing, anti-fingerprinting, and massive parallel tasking.

## Hardware Used

- 12x Raspberry Pi 4 (8GB RAM)
- 2x Nvidia Jetson Nano (4GB)
- 14x Raspberry Pi Compute Module 3 (on 2x Turing Pi cluster boards)
- 3x Raspberry Pi Compute Module 4 (on PoE carrier boards)
- 1x Drobo 800fs NAS (18TB storage)
- 2x Managed Gigabit Switches
- 1x PowerSpec B732 Desktop (Control/Brain node)

## Networking

- VLAN segmentation for Storage, Node, and Management traffic
- VPN exit traffic (PIA + NordVPN) rotated every 30 minutes
- OpenWRT configured on one CM4 node to manage all VPN traffic

## Features

- Fully Kubernetes managed
- MetalLB for load balancing
- Calico for network overlay
- Full air-gap internal communications
- Randomized hostnames, MAC addresses, and IPs
- Anti-fingerprinting and IP poison-avoidance scripts

## Deployment

See `deployment_notes.md` for full wiring, network, and bootstrap instructions.

## Why?

Because real clusters don't live in the cloud — they live **under your desk, breathing fire**.

---
