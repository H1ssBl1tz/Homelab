# WireGuard Setup

## Purpose

WireGuard links the physical Kali workstation to the Windows machine hosting the isolated target network.

```text
Windows: 10.200.0.1
Kali:    10.200.0.2
```

## Key Generation — Kali

```bash
umask 077
wg genkey | tee privatekey | wg pubkey > publickey
```

Display only the public key when exchanging peer information:

```bash
cat publickey
```

Never publish `privatekey`.

## Key Ownership

```text
Windows PrivateKey → Windows only
Windows PublicKey  → may be configured on Kali

Kali PrivateKey    → Kali only
Kali PublicKey     → may be configured on Windows
```

## Example Configurations

Sanitized examples are available under [`configs/wireguard/`](../configs/wireguard/).

### Kali

Typical file:

```text
/etc/wireguard/wg0.conf
```

Bring the interface up:

```bash
sudo wg-quick up wg0
```

Check status:

```bash
sudo wg
ip addr show wg0
```

Bring it down:

```bash
sudo wg-quick down wg0
```

## Validation

From Kali:

```bash
ping 10.200.0.1
sudo wg
```

A recent `latest handshake` plus transfer counters confirms that the peers are exchanging traffic.
