# Troubleshooting

This document records the network issues encountered while building the lab and the checks that resolved them.

## 1. WireGuard Addresses Reversed

Correct assignment:

```text
Windows = 10.200.0.1
Kali    = 10.200.0.2
```

A peer may appear configured while routing still fails if the logical addressing plan is inconsistent.

## 2. Incorrect Peer Keys

Symptoms can include a tunnel with no usable handshake.

Check:

```bash
sudo wg
```

If `latest handshake` is missing, review:

- the peer public keys;
- endpoint address/port;
- local firewall;
- which machine owns each private key.

## 3. Incomplete `AllowedIPs`

Kali must know that the VirtualBox network is reachable through the Windows WireGuard peer.

```ini
AllowedIPs = 10.200.0.0/24, 192.168.56.0/24
```

Check the resulting routes:

```bash
ip route
```

## 4. Windows Was Not Forwarding Traffic

A working WireGuard handshake only proves that the VPN peers can communicate. It does not automatically make Windows route traffic into the Host-Only network.

Review:

- forwarding state on both interfaces;
- correct interface aliases;
- Windows Firewall rules;
- route tables.

## 5. Missing Return Route on Metasploitable3

Symptom:

```text
Windows reaches the VM, but Kali cannot complete communication.
```

Fix:

```bash
sudo ip route add 10.200.0.0/24 via 192.168.56.1
```

## Diagnostic Checklist

```text
[ ] wg0 is active on Kali
[ ] WireGuard shows a recent handshake
[ ] Kali can ping 10.200.0.1
[ ] Windows can ping 192.168.56.10
[ ] Kali has a route for 192.168.56.0/24
[ ] Windows forwarding is enabled
[ ] Windows Firewall permits required lab traffic
[ ] Metasploitable3 has a route for 10.200.0.0/24
[ ] Target VM is attached only to the intended lab network
[ ] Addresses match the documented plan
```

### Kali

```bash
ip addr
ip route
sudo wg
ping 10.200.0.1
ping 192.168.56.10
```

### Windows

```powershell
ipconfig
route print
Get-NetIPInterface -AddressFamily IPv4
ping 192.168.56.10
```

### Metasploitable3

```bash
ip addr
ip route
ping 192.168.56.1
```
