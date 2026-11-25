<div align="center">

<img src="https://github.com/mygate-ips.png" width="120" alt="MyGate logo">

# MyGate

**An AI-powered network security appliance (IPS)**

Signature-based detection with Suricata · Flow-based detection with machine learning · Automatic blocking with nftables

Graduation project · Electrical & Computer Engineering · Benha University

</div>

---

## What it does

MyGate sits in front of a local network, watches every connection, and stops attacks on its own.

```
 LAN traffic
     │
     ├──► Suricata ───────────► signatures: SQLi, XSS, scanners, floods ...
     │
     ├──► Flow extractor ─► ML model ─► port scan · brute force · DoS
     │
     ▼
 Decision engine ──► alert (≥ 0.5) · temporary block (≥ 0.9) · trusted IPs never blocked
     │
     ▼
 nftables  ·  Web dashboard  ·  CLI  ·  Telegram alerts
```

- **Two detection layers.** Suricata catches known attack patterns per packet; a Random Forest trained on 1.7M CIC-IDS2017 flows catches attack *behaviour* per connection.
- **Policy engine.** Three modes (`alert_only` · `manual` · `automatic`), temporary blocks that expire on their own, escalating blocks for repeat attackers, and a trusted-IP list.
- **Built for a real appliance.** Runs on Ubuntu Server 24.04, every component as its own service, all actions going through one core so the dashboard, CLI and bot never touch the firewall directly.

## Team

| Area | Responsibility |
|---|---|
| **Core** | Controllers, event bus, decision engine, database |
| **AI / ML** | Detection model, live flow extraction, evaluation |
| **Network & Security** | Server setup, Suricata rules, firewall, attack simulation |
| **Web** | REST API, authentication, dashboard |
| **Cloud** | Deployment, services, backups |

## Stack

Python · scikit-learn · Scapy · CICFlowMeter · Suricata · nftables · PostgreSQL · FastAPI · Docker · Ubuntu Server

## How we work

Every change goes through a branch and a pull request, gets reviewed, and only then reaches `main`. See [CONTRIBUTING.md](https://github.com/mygate-ips/MyGate/blob/main/CONTRIBUTING.md).
