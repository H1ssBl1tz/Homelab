# Architecture

## Objective

The lab was designed to provide an isolated, reproducible environment for cybersecurity practice while keeping intentionally vulnerable systems away from the normal home LAN.

## Current Components

| Component | Role |
|---|---|
| Kali Linux | Physical attacker workstation |
| Windows 11 | Virtualization host and router between lab networks |
| WireGuard | VPN between Kali and the Windows host |
| VirtualBox | Hypervisor for vulnerable targets |
| Host-Only Adapter | Isolated target segment |
| Metasploitable3 | Current intentionally vulnerable target |

## Traffic Flow

```mermaid
flowchart LR
    KALI["Kali Linux\n10.200.0.2"]
    WG["WireGuard"]
    WIN["Windows 11\n10.200.0.1"]
    VBOX["Host-Only\n192.168.56.1"]
    META["Metasploitable3\n192.168.56.10"]

    KALI --> WG --> WIN --> VBOX --> META
```

The Windows host is the routing point between two distinct networks:

```text
10.200.0.0/24     WireGuard segment
192.168.56.0/24   VirtualBox lab segment
```

## Isolation Model

Preferred:

```text
Normal network
     │
Kali / Windows
     │
WireGuard + controlled routing
     │
VirtualBox Host-Only
     │
Vulnerable VM
```

Avoid:

```text
Home router
     │
Bridged Adapter
     │
Intentionally vulnerable VM
```

The target VM does not need to be directly reachable from the normal LAN to support the lab's objectives.
