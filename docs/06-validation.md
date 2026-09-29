# Validation

Validation is performed layer by layer so a failure can be isolated quickly.

## Test 1 — Kali → Windows WireGuard

From Kali:

```bash
ping 10.200.0.1
```

Expected:

```text
PASS
```

## Test 2 — Windows → Metasploitable3

From Windows:

```powershell
ping 192.168.56.10
```

Expected:

```text
PASS
```

## Test 3 — Kali → Metasploitable3

From Kali:

```bash
ping 192.168.56.10
```

Expected:

```text
PASS
```

When all three pass, the complete path is operational:

```text
Kali
  ↓
WireGuard
  ↓
Windows routing
  ↓
VirtualBox Host-Only
  ↓
Metasploitable3
```

## Initial Enumeration

Basic target discovery:

```bash
nmap -Pn 192.168.56.10
```

Service detection:

```bash
nmap -sV -Pn 192.168.56.10
```

Default scripts + versions:

```bash
nmap -sC -sV -Pn 192.168.56.10
```

The purpose of this stage is to confirm that Kali can reach and enumerate the services exposed by the lab target.
