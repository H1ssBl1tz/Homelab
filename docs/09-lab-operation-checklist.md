# Lab Operation Checklist

Use this checklist whenever starting or shutting down the lab.

## Before a Session

### 1. Start the Windows Host

Confirm that the VirtualBox Host-Only adapter still uses the documented lab address:

```text
192.168.56.1/24
```

Useful command:

```powershell
ipconfig
```

### 2. Start the Target VM

Boot Metasploitable3 and verify:

```bash
ip addr
ip route
```

Expected target address:

```text
192.168.56.10/24
```

Expected return route:

```text
10.200.0.0/24 via 192.168.56.1
```

If the route was not made persistent and is missing:

```bash
sudo ip route add 10.200.0.0/24 via 192.168.56.1
```

### 3. Validate Windows ↔ Target

From Windows:

```powershell
ping 192.168.56.10
```

Do not continue until the Windows host can reach the VM.

### 4. Start WireGuard

Enable the Windows WireGuard tunnel, then on Kali:

```bash
sudo wg-quick up wg0
```

Verify:

```bash
sudo wg
```

Look for a recent handshake.

### 5. Validate Kali ↔ Windows

```bash
ping 10.200.0.1
```

### 6. Validate Kali ↔ Target

```bash
ping 192.168.56.10
```

If this fails, work through [`07-troubleshooting.md`](07-troubleshooting.md) instead of changing multiple settings at once.

### 7. Begin the Lab Session

Once the network path is validated, start the required tooling from Kali.

Example baseline check:

```bash
nmap -sV -Pn 192.168.56.10
```

## After a Session

1. Stop active listeners, scans, and lab tooling.
2. Save only sanitized notes/evidence intended for the repository.
3. Shut down or suspend the vulnerable VM.
4. On Kali, bring down the tunnel when it is no longer needed:

```bash
sudo wg-quick down wg0
```

5. Disable the Windows WireGuard tunnel if the lab is finished.
6. Keep vulnerable targets off bridged networking.

## Quick Health Check

```text
[ ] Target uses Host-Only, not Bridged
[ ] Windows → target works
[ ] WireGuard handshake exists
[ ] Kali → Windows works
[ ] Return route exists on target
[ ] Kali → target works
[ ] No secrets are being recorded in screenshots/logs
```
