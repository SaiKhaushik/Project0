# Secure Internship
Secure MAVLink Communication for UAVs

## Overview

It focuses on identifying security vulnerabilities in the MAVLink communication protocol used by Unmanned Aerial Vehicles (UAVs) and designing a secure communication framework to improve message confidentiality, integrity, and authenticity. We combined simulation testing with cryptographic techniques to analyze attacks on MAVLink communication to find respective solutions.

---

## Objectives

- To study the MAVLink communication protocol.
- Identifying vulnerabilities present in MAVLink 2.0.
- Simulating UAV communication virtually.
- Analyzing common cyber attacks targeting UAV communication.
- Designing and evaluating secure communication mechanisms.
- Comparing existing approaches with the proposed solution.

---

## Simulation Tools

| Component | Purpose |
|-----------|---------|
| PX4 Autopilot | Flight controller simulator |
| Gazebo | UAV simulation environment |
| QGroundControl | Ground Control Station |
| MAVProxy | MAVLink communication interface |
| PyMAVLink | Python-based MAVLink communication |
| Wireshark | Packet capture and protocol analysis |

---

## Vulnerabilities Studied

- Eavesdropping
- Packet Tampering
- Forged Packet
- Man-in-the-Middle (MITM) Injection
- Command Spoofing
- Replay Attack
- Predictable Nonce Attack
- Token Brute Force
- Stale Token Replay
- Rate-Limit / Lockout Bypass
- GPS AAD Tampering
- Hardcoded Key Discovery
- Nonce Reuse Catastrophe

---

## Security Techniques Evaluated

- Two-Factor Authentication (2FA)
- Affine Cipher (Initial Study)
- HMAC with SHA-256
- ChaCha20-Poly1305 Authenticated Encryption
