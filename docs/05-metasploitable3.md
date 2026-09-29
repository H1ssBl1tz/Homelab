# Metasploitable3

## Role

Metasploitable3 is the first intentionally vulnerable target in the lab.

## Network Configuration

```text
Interface: eth0
Address:   192.168.56.10/24
Network:   VirtualBox Host-Only
```

The lab was configured without relying on a normal default route to the Internet.

To reply to the Kali WireGuard network, the VM needs the following route:

```bash
sudo ip route add 10.200.0.0/24 via 192.168.56.1
```

Check the configuration:

```bash
ip addr
ip route
```

## Default Lab Credentials

For the standard Metasploitable3 Ubuntu/Vagrant environment used during setup:

```text
Username: vagrant
Password: vagrant
```

These credentials belong to an intentionally vulnerable training VM. Never reuse them on real systems.

## Current Goal

At this stage the target is used to validate connectivity, service discovery, enumeration, and controlled lab exercises.
