# Roadmap

The lab is intended to evolve from a networking/pentest environment into a larger Red + Blue security platform.

## Phase 1 — Network Infrastructure ✅

- [x] Define the physical Kali attacker workstation
- [x] Configure Windows as virtualization host
- [x] Create VirtualBox Host-Only network
- [x] Configure Metasploitable3
- [x] Configure static addressing
- [x] Configure WireGuard
- [x] Establish WireGuard handshake
- [x] Enable Kali ↔ Windows communication
- [x] Enable Windows ↔ Metasploitable3 communication
- [x] Enable Windows forwarding
- [x] Add target return route
- [x] Enable Kali ↔ Metasploitable3 communication

## Phase 2 — Vulnerable Linux Targets 🚧

Potential targets:

```text
Metasploitable2
Metasploitable3 Linux
```

Focus:

- enumeration;
- Linux services;
- known vulnerabilities;
- controlled post-exploitation;
- evidence collection and remediation notes.

## Phase 3 — Web Security

Potential lab targets:

```text
DVWA
OWASP Juice Shop
WebGoat
Custom vulnerable applications
```

Focus:

- HTTP behavior;
- authentication;
- access control;
- SQL injection;
- XSS;
- IDOR;
- Burp Suite analysis.

## Phase 4 — Windows Security

Add a Windows target such as Metasploitable3 Windows.

Focus:

- SMB / RPC enumeration;
- Windows services;
- PowerShell;
- controlled exploitation;
- post-exploitation inside the lab.

## Phase 5 — Active Directory

Planned domain:

```text
CORP.LOCAL
```

Planned systems:

```text
DC01  → Windows Server / AD DS / DNS
WS01  → Domain-joined workstation
SRV01 → Domain-joined server
```

Focus:

- LDAP;
- Kerberos;
- DNS;
- Group Policy;
- users and groups;
- AD enumeration;
- attack and detection exercises within the lab.

## Phase 6 — Blue Team Telemetry

Planned direction:

```text
Endpoints
   ↓
Sysmon
   ↓
Wazuh Agent
   ↓
Wazuh / SIEM
   ↓
Detection and analysis
```

Focus:

- event visibility;
- log analysis;
- detection rules;
- MITRE ATT&CK mapping;
- correlating offensive actions with defensive telemetry.

## Long-Term Goal — Purple Team Lab

The final environment should make it possible to execute an authorized technique, collect the resulting telemetry, understand why a detection did or did not trigger, and document both the attack path and the defensive response.
