# Network Design

## Addressing Plan

| System | Interface / Function | Address |
|---|---|---|
| Kali Linux | WireGuard | `10.200.0.2/24` |
| Windows 11 | WireGuard | `10.200.0.1/24` |
| Windows 11 | VirtualBox Host-Only | `192.168.56.1/24` |
| Metasploitable3 | `eth0` | `192.168.56.10/24` |

## Networks

```text
WireGuard VPN:       10.200.0.0/24
VirtualBox lab:      192.168.56.0/24
```

## Windows Forwarding

List IPv4 interfaces before changing anything:

```powershell
Get-NetIPInterface -AddressFamily IPv4
```

Enable forwarding on the WireGuard and Host-Only interfaces:

```powershell
Set-NetIPInterface `
  -InterfaceAlias "<WIREGUARD_INTERFACE>" `
  -Forwarding Enabled

Set-NetIPInterface `
  -InterfaceAlias "<VIRTUALBOX_HOST_ONLY_INTERFACE>" `
  -Forwarding Enabled
```

Verify:

```powershell
Get-NetIPInterface -AddressFamily IPv4 |
    Select-Object InterfaceAlias,Forwarding
```

Interface names vary between installations. Resolve the actual aliases before running the commands.

## Return Route

The Kali-to-target path is not enough on its own. Metasploitable3 also needs a route back to the WireGuard network.

```bash
sudo ip route add 10.200.0.0/24 via 192.168.56.1
```

Verify:

```bash
ip route
```

Expected entry:

```text
10.200.0.0/24 via 192.168.56.1
```

Without this route, traffic may reach the VM while replies fail to return to Kali.
