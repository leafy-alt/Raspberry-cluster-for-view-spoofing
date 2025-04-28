Project Hydra: RPi + Jetson Cluster Traffic Lab

Overview

Project Hydra is a semi-airgapped distributed compute cluster built to experiment with network traffic simulation, YouTube view count spoofing, anti-fingerprinting techniques, and cluster-level evasion strategies.

The cluster was architected around performance-first, high churn rates, and operational stealth — real-world hardware, real-world tactics.


---

Hardware Used

12x Raspberry Pi 4B (8GB RAM models)

2x NVIDIA Jetson Nano (4GB models)

2x Turing Pi Cluster Boards populated with:

14x Raspberry Pi Compute Module 3 (CM3)


3x Raspberry Pi Compute Module 4 (CM4) with PoE Carrier Boards

1x PowerSpec B732 Workstation (Controller Node / Brain)

1x Drobo 800fs NAS (18TB of Network Storage)

Various unmanaged gigabit switches

VPN Router Setup:

Private Internet Access (PIA) VPN

NordVPN


1x OpenWRT Router:

Hosted on one CM4 module to manage all VPN tunnels, DNS masking, and custom routing policies.




---

Software Stack

Kubernetes (k8s) used to orchestrate the cluster across all nodes.

Custom Bash and Python scripts to handle:

IP rotation

Process recycling

Node health monitoring


OpenWRT on a CM4 for routing and VPN gateway management.

Storage Access: NFS mounts linked to Drobo 800fs for shared persistence.



---

Architecture

Networking:

Nodes segmented into VLANs for isolation.

External internet traffic was routed over dual-layered VPNs (PIA + NordVPN) for diversified egress.

The OpenWRT CM4 router dynamically managed tunnel assignments and DNS split-horizon policies.


IP Rotation / Fingerprint Defense:

Every 30 minutes, nodes were cycled:

Fresh network stack install.

New VPN server connection.

New device identifiers (MAC spoofing / hostname rotation).


Goal: eliminate static signatures that could be used to detect fake views or cluster behavior.


Storage:

The Drobo 800fs NAS provided 18TB of networked persistent storage for logs, payloads, and automation scripts.


Cluster Brain:

The PowerSpec B732 handled k8s master duties, orchestration, and served as the centralized control plane.




---

Purpose

Originally built as a free service to boost YouTube view counts for smaller creators who needed help breaking algorithm barriers — without asking for payment.
Spoiler alert: people don't trust free miracles, even when you're legit.


---

Future Expansion Ideas

Integrate TOR exit nodes for even deeper anonymity.

Create auto-healing node pools when VPN tunnels die or nodes fingerprint.

Move controller node to a dedicated rackmount server for greater scale.



---

Notes to Replicators

If you plan to replicate this project:

Expect hardware costs. (You’ll need about 20+ real devices or strong virtualization skills.)

Expect heat + electricity bills. (Clusters are noisy little bastards.)

Expect troubleshooting. (It's half the job.)


Pro Tip: Airgapping improves cluster stability and realism — but makes remote management trickier. Use an OpenWRT head node like I did to keep your hands clean.
