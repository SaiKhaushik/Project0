# Simulated Software Attacks

## 1. Eavesdropping Attack

### Description
An attacker intercepts wireless communication and attempts to read sensitive information from transmitted packets without modifying them.

### Objective
Recover plaintext such as GPS coordinates, commands, or telemetry.

### Defense
ChaCha20 encrypts all payload data, making intercepted packets appear as random ciphertext.

### Result
✅ Blocked – No plaintext information is exposed.


---

## 2. Packet Tampering Attack

### Description
An attacker captures a legitimate encrypted packet and modifies one or more bits before forwarding it to the receiver.

### Objective
Alter commands without knowing the encryption key.

### Defense
Poly1305 authentication verifies packet integrity. Any modification changes the authentication tag.

### Result
✅ Blocked – MAC verification fails and the packet is discarded.


---

## 3. Forged Packet Attack

### Description
An attacker creates a completely fake encrypted packet and sends it to the receiver.

### Objective
Inject unauthorized commands into the communication channel.

### Defense
Without the shared secret key, the attacker cannot generate a valid Poly1305 authentication tag.

### Result
✅ Blocked – Forged packets are rejected.


---

## 4. Man-in-the-Middle (MITM) Injection

### Description
An attacker positions themselves between the sender and receiver, intercepting and modifying packets before forwarding them.

### Objective
Manipulate transmitted commands while remaining undetected.

### Defense
Every packet is authenticated using Poly1305. Any modification invalidates the MAC.

### Result
✅ Blocked – Modified packets fail authentication.


---

## 5. Command Spoofing Attack

### Description
An attacker attempts to send fake drone commands pretending to be a legitimate Ground Control Station.

### Objective
Take control of the drone by issuing unauthorized commands.

### Defense
Only devices possessing the correct secret key can generate valid authenticated packets.

### Result
✅ Blocked – Spoofed commands are rejected.


---

## 6. Replay Attack

### Description
An attacker records a legitimate encrypted packet and retransmits it later.

### Objective
Repeat previously valid commands.

### Defense
Every packet uses a unique nonce. Previously used nonces are stored and rejected if reused.

### Result
✅ Blocked – Duplicate packets are detected immediately.


---

## 7. Predictable Nonce Attack

### Description
An attacker analyzes nonce generation hoping to predict future nonces.

### Objective
Exploit predictable nonces to weaken encryption.

### Defense
Random cryptographically secure nonce generation ensures uniqueness and unpredictability.

### Result
✅ Blocked – Generated nonces remain unique.


---

## 8. Token Brute Force Attack

### Description
An attacker repeatedly guesses authentication tokens.

### Objective
Gain unauthorized access by guessing a valid token.

### Defense
Large token space (2^56) makes brute-force computationally infeasible.

### Result
✅ Blocked – No successful guesses.


---

## 9. Stale Token Replay Attack

### Description
An attacker attempts to reuse an expired authentication token.

### Objective
Authenticate using an old but previously valid token.

### Defense
Tokens include timestamps and are accepted only within a predefined validity window.

### Result
✅ Blocked – Expired tokens are rejected.


---

## 10. Rate-Limit / Lockout Attack

### Description
An attacker performs repeated authentication attempts to guess credentials.

### Objective
Eventually authenticate through repeated failures.

### Defense
After multiple failed attempts, the system temporarily locks further authentication requests.

### Result
✅ Blocked – Lockout mechanism activated.


---

## 11. GPS AAD Tampering Attack

### Description
An attacker modifies GPS coordinates that are included as Additional Authenticated Data (AAD).

### Objective
Redirect or manipulate drone navigation without changing the encrypted payload.

### Defense
AAD is authenticated by Poly1305. Any modification changes the authentication tag.

### Result
✅ Blocked – Authentication fails and the packet is discarded.


---

## 12. Hardcoded Key Discovery

### Description
An attacker examines the application's source code looking for embedded encryption keys.

### Objective
Recover secret cryptographic keys directly from the program.

### Defense
No cryptographic keys are hardcoded inside the source code.

### Result
✅ Blocked – No embedded keys found.


---

## 13. Nonce Reuse Catastrophe

### Description
Nonce reuse in stream ciphers can reveal information about the plaintext and compromise encryption security.

### Objective
Exploit reused nonces to recover encrypted data.

### Defense
Every encryption operation generates a fresh unique nonce, even for identical messages.

### Result
✅ Blocked – Identical plaintexts produce different ciphertexts every time.


# Residual Hardware / Physical Attacks

## 1. RF Jamming

### Description
An attacker transmits powerful radio signals on the communication frequency, preventing legitimate communication.

### Objective
Disrupt communication between the Ground Control Station and the UAV.

### Software Defense
None.

### Hardware Mitigation
- Frequency Hopping Spread Spectrum (FHSS)
- Adaptive frequency selection
- Directional antennas
- Higher transmission power

### Result
⚠ Cannot be prevented by encryption alone.


---

## 2. GPS Spoofing

### Description
An attacker broadcasts counterfeit GPS signals stronger than legitimate satellite signals.

### Objective
Cause the drone to calculate an incorrect position and navigate to a false location.

### Software Defense
GPS coordinates can be authenticated during transmission, but fake satellite signals cannot be detected solely through encryption.

### Hardware Mitigation
- Multi-constellation GNSS
- IMU and sensor fusion
- Anti-spoofing GNSS receivers
- RTK GPS

### Result
⚠ Requires specialized navigation hardware.


---

## 3. Endpoint Compromise

### Description
An attacker gains physical or software access to the drone or Ground Control Station.

### Objective
Steal secret keys, modify firmware, or bypass cryptographic protection.

### Software Defense
Limited.

### Hardware Mitigation
- Secure Boot
- Hardware Security Module (HSM)
- Trusted Platform Module (TPM)
- Secure firmware signing
- Trusted Execution Environment (TEE)

### Result
⚠ Cryptography cannot protect a compromised endpoint.
