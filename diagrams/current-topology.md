# Current Topology

```mermaid
flowchart LR
    KALI["Kali Linux<br/>Physical attacker<br/>10.200.0.2"]
    WG["WireGuard<br/>10.200.0.0/24"]
    WIN["Windows 11 Host<br/>Router + Hypervisor<br/>10.200.0.1"]
    HOSTONLY["VirtualBox Host-Only<br/>192.168.56.1"]
    META["Metasploitable3<br/>192.168.56.10"]

    KALI --> WG --> WIN --> HOSTONLY --> META
```

## Return Path

```text
Metasploitable3 192.168.56.10
        │
        └─ route 10.200.0.0/24 via 192.168.56.1
                       │
                 Windows router
                       │
                   WireGuard
                       │
                  Kali 10.200.0.2
```
