# Security Policy

## Scope

This repository documents an intentionally vulnerable cybersecurity lab.

The material is intended for:

- systems you own;
- intentionally vulnerable virtual machines;
- CTF and training environments;
- environments where explicit authorization has been granted.

Do not use techniques from this repository against third-party infrastructure without authorization.

## Secrets

No real credentials, private keys, public endpoints, private DDNS names, or production configuration files should be committed.

If a secret is accidentally committed:

1. rotate or revoke it immediately;
2. remove it from the current repository state;
3. clean it from Git history when necessary;
4. verify that no derived credential remains valid.

## Reporting a Repository Issue

If you notice that a committed file exposes information that should have been sanitized, open a GitHub issue without reproducing the secret itself.
