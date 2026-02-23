# Building-a-Three-Site-Enterprise-Network-from-Scratch
Not just the commands — the why behind every decision, and what to do when things break. Written for the IT 381/481 student who will struggle exactly where I did.
# IT 481 — Multi-Site OSPF Lab Tutorial
### Building a Three-Site Enterprise Network from Scratch

**Author:** Oma Nlerum  
**Course:** IT 481 · Lab 06 · 2026  
**Published for:** Future IT 481 students

---

## 👉 [View the Full Tutorial →](./index.html)

---

## What This Is

This is not just a lab writeup.

This is the guide I wish I had before I started Lab 06 — written specifically for future IT 481 students who will struggle exactly where I did. Every command is explained. Every mistake I made is documented. Every fix is included.

> *"You are not writing this for marks. You are writing this for future IT 481 students who will struggle exactly where you did."*

---

## What the Lab Builds

A **three-site enterprise network** — the kind that exists in every real company with multiple offices:


        ┌─────────────────┐
        │   R1 — HQ-Site  │  Loopback: 142.1.64.254
        │   VLAN 100      │
        └────────┬────────┘
                 │
        ┌────────┴────────┐
        │                 │
┌───────┴──────┐   ┌──────┴───────┐
│ R2 — Site-B  │   │ R3 — Site-C  │
│ VLAN 200     │───│ VLAN 300     │
└──────────────┘   └──────────────┘

WAN Links:  10.12.1.0/30 · 10.13.1.0/30 · 10.23.1.0/30
OSPF:       Area 0 · Full mesh routing


---

## Skills Covered

| Technology | What You Learn |
|---|---|
| **VLANs** | Create and name VLANs, assign access ports, configure trunk ports |
| **Router-on-a-Stick** | Sub-interfaces, encapsulation dot1Q, parent interface rules |
| **OSPF** | Dynamic routing, network statements, wildcard masks, passive-interface |
| **WAN Links** | /30 subnets for point-to-point links between routers |
| **Loopback Interfaces** | Stable OSPF router-IDs that never go down |
| **IOL PC Nodes** | Configure Cisco IOL routers as end devices with default routes |

---

## What's Inside the Tutorial

| Section | Content |
|---|---|
| 01 Introduction | What the lab teaches, mindset for success |
| 02 Network Topology | Full SVG diagram, IP address reference table |
| 03 Switch Config | SW1/SW2/SW3 — VLANs, access ports, trunk ports |
| 04 Router Config | R1/R2/R3 — loopbacks, sub-interfaces, WAN links |
| 05 OSPF Config | All three routers, wildcard masks explained |
| 06 PC Config | IOL router vs VPCS, default routes explained |
| 07 Verification | OSPF neighbor states, routing tables, ping tests |
| 08 Troubleshooting | 5 real problems I hit with exact fixes |
| 09 Conclusion | Bottom-up debugging mindset, key lessons |

---

## Devices Configured

| Device | Role | Key Interfaces |
|---|---|---|
| SW1 | HQ switch | VLAN 100, access e0/1, trunk e0/0 |
| SW2 | Site-B switch | VLAN 200, access e0/1, trunk e0/0 |
| SW3 | Site-C switch | VLAN 300, access e0/1, trunk e0/0 |
| R1 | HQ router | e0/0.100, e0/2 (WAN-R2), e0/3 (WAN-R3) |
| R2 | Site-B router | e0/0.200, e0/2 (WAN-R1), e0/1 (WAN-R3) |
| R3 | Site-C router | e0/0.300, e0/3 (WAN-R1), e0/1 (WAN-R2) |
| PC1 | HQ workstation | 142.100.64.11 · GW: 142.100.64.1 |
| PC2 | Site-B workstation | 142.100.65.21 · GW: 142.100.65.1 |
| PC3 | Site-C workstation | 142.100.66.31 · GW: 142.100.66.1 |

---

## The 5 Mistakes I Made (So You Don't Have To)

1. **Using VPCS syntax on an IOL PC** — fails silently, nothing gets configured
2. **Wrong VLAN on the trunk** — SW2 was allowing VLAN 100 instead of 200
3. **Forgetting `no shutdown` on the parent interface** — sub-interfaces stay down with no obvious cause
4. **Wrong VLAN names** — "vlan1" instead of "HQ-VLAN" costs Task 2 marks
5. **Missing loopback in OSPF network statements** — loopbacks unreachable from PCs

---

## How to Use This Tutorial

1. Open `IT481_Tutorial_OmaNlerum.html` in any browser
2. Keep the IP reference table (Section 02) open the whole time
3. Configure in order: Switches → Routers → OSPF → PCs
4. Verify after each device with `show` commands before moving on
5. If something breaks, check Section 08 — Troubleshooting

---

## Lab Environment

- **Platform:** GNS3 / EVE-NG with Cisco IOL images
- **PC nodes:** Cisco IOL routers acting as end devices (not VPCS)
- **Switch images:** IOL L2 switches (require `encapsulation dot1q` before trunk mode)
- **Routing protocol:** OSPFv2, single Area 0

---

## For Future IT 481 Students

If this tutorial helped you — pay it forward.

Write your own version when you're done. Add the mistakes you made that aren't in this one. Publish it. Leave it for the next person.

That's how we all get better.

---

*Oma Nlerum · IT 481 · 2026*
