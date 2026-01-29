# VLANs & Inter-VLAN Routing Lab

This lab documents the setup and verification of VLAN segmentation and
inter-VLAN routing in a small enterprise-style network.

## Goal
- Segment a network into multiple VLANs for separation of users/services
- Enable controlled communication between VLANs using inter-VLAN routing
- Verify correct forwarding, gateway configuration, and trunk behaviour

## Scenario (Example)
- VLAN 10: Users
- VLAN 20: Admin
- VLAN 30: Servers
- One Layer 2 switch (access ports + trunk)
- One router or Layer 3 device providing inter-VLAN routing

## Key Concepts
- **Access port**: carries traffic for a single VLAN
- **Trunk port**: carries traffic for multiple VLANs (802.1Q tagging)
- **SVI / Subinterfaces**: provide default gateways per VLAN
- **Inter-VLAN routing**: allows VLANs to communicate via a routed interface

## Steps Performed (High Level)
1. Created VLANs and assigned switch access ports to the correct VLANs.
2. Configured the switch uplink as a trunk to carry VLAN 10/20/30.
3. Configured inter-VLAN routing using:
   - Router-on-a-stick (subinterfaces + 802.1Q), or
   - Layer 3 switch SVIs (depending on lab setup).
4. Assigned end hosts correct IP addresses and default gateways per VLAN.
5. Verified connectivity:
   - Same-VLAN communication works (L2 switching)
   - Inter-VLAN communication works (L3 routing)
6. Confirmed VLAN tagging and trunk operation using show commands.

## Verification Checklist
- `show vlan brief` shows expected VLANs and port membership
- `show interfaces trunk` confirms trunk is up and allowed VLANs match
- `show ip interface brief` confirms L3 interfaces/SVIs are up/up
- Ping tests:
  - Host → default gateway (same VLAN)
  - Host in VLAN 10 → host in VLAN 20/30 (inter-VLAN)
- If something fails:
  - Check access VLAN on ports
  - Check trunk allowed VLAN list
  - Check gateway IP/subinterface tagging
  - Check host default gateway and IP/subnet mask

## What I Learned
- VLANs reduce broadcast domain size and improve segmentation.
- Inter-VLAN routing must be explicitly configured; VLANs do not route by default.
- Most issues come from misconfigured trunks (allowed VLANs / tagging) or
  incorrect default gateways on hosts.
