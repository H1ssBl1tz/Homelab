# VirtualBox Host-Only Network

## Goal

VirtualBox hosts the intentionally vulnerable targets on a network that is isolated from the normal LAN.

## Host-Only Adapter

Example Windows-side address:

```text
IPv4: 192.168.56.1
Mask: 255.255.255.0
```

Current lab network:

```text
192.168.56.0/24
```

## Target Adapter

Metasploitable3 uses:

```text
Adapter 1 → Host-Only Adapter
```

After booting the VM:

```bash
ip addr
```

Expected target address:

```text
192.168.56.10/24
```

## Host Validation

From Windows:

```powershell
ping 192.168.56.10
```

If this succeeds, the local path between the Windows host and the target VM is working.

## Safety Rule

Do not use **Bridged Adapter** as the primary interface for an intentionally vulnerable machine in this lab.
