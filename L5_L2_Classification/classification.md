# L5 Narrow / L2 General Classification — web-extension
**Platform:** Anticloud | **PAX:** 27B | **IP:** USPTO pending 2026, Anticloud FZ LLE
**Domain:** Sovereign browser extension: local AI assistant powered by PAX 27B via LAN API

## L5 Narrow
web-extension specializes in sovereign browser extension: local ai assistant powered by pax 27b via lan api within the Anticloud sovereign deployment boundary. All operations stay local — no cloud services, no external APIs, no data exfiltration. The narrow scope ensures deterministic, auditable behavior that PAX 27B can reason about precisely.

## L2 General
L2 General means web-extension is available to all 9 Anticloud tiers without per-tier configuration. The same API serves hospital, defense, robotics, and research deployments.

## PAX Integration
PAX 27B responds to extension queries entirely via LAN WebSocket: no data leaves the local network. The extension calls ws://192.168.x.x:8081/chat, not any cloud endpoint.

## AIOSS Audit Relevance
Every extension interaction (page domain hash + query hash + PAX response hash) is AIOSS-chained: H_n = SHA3-256(H_{n-1} || entry_hash_n || timestamp_n).
Tamper-evident, offline-verifiable, zero cloud dependency.

## Regulatory / Compliance
GDPR Art. 25 (extension: no external API calls, LAN only), CCPA, browser extension CSP
