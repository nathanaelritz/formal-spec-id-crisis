# Formal Analysis of Standalone Idealized KEM Integration in TLS 1.3

This repository extends the formal-spec-id-crisis models by Sardar, Moustafa, and Aura ([Apache 2.0](https://github.com/CCC-Attestation/formal-spec-id-crisis/tree/main)), which themselves build on the original TLS 1.3 ProVerif [reftls](https://github.com/Inria-Prosecco/reftls/blob/master/pv/tls-lib.pvl) library by Bhargavan, Blanchet, and Kobeissi. `../TLS-a/tls-lib-simple.pvl` is a close fork, extended with post-handshake application data modeling and a structured query architecture aligned to replicate the attacks disclosed with [CVE-2026-33697](https://github.com/ultravioletrs/cocos/security/advisories/GHSA-vfgg-mvxx-mgg7). The `./pq-kem/` models replace the idealized DHE primitive with an idealized KEM abstraction, holding all other structural elements constant.

The repository is a controlled 2×2 comparison between an **idealized Diffie-Hellman key exchange** and an **idealized KEM abstraction** in TLS 1.3 intra-handshake remote attestation, evaluated across two protocol states: a known vulnerable protocol and its mitigation.

At the symbolic level used by ProVerif, neither primitive is modeled by its concrete mathematics. The idealized DHE is an abstract commutative group operation; the idealized KEM is an abstract asymmetric encapsulation and decapsulation pair. The comparison is between those two abstractions — their structural properties and how they interact with the protocol's security guarantees — not between specific cryptographic implementations.

**Question in scope:** Does replacing an idealized DHE with an idealized KEM abstraction introduce novel attack surfaces or alter the security properties of the protocol?

**Analysis:** None found based on the model. The verification confirms strict, one-to-one structural parity between the idealized DHE and idealized KEM implementations across all organized queries per verification target. The primitive transition introduces no novel vulnerabilities and breaks no existing security boundaries.

---

## Repository Structure

The repository is organized as a 2×2 matrix: two cryptographic primitives (idealized DHE, idealized KEM) × two protocol states (vulnerable, mitigated), yielding four distinct verification targets:

|                  | Idealized DHE   | Idealized KEM    |
|------------------|-----------------|------------------|
| **Vulnerable** | `../TLS-a`   | `./cve/`    |
| **Mitigated** | `..TLS-a/fix/`        | `./fix/`    |

The DHE column establishes the baseline. The KEM column runs the same query set against the same protocol structure with the primitive replaced. Differences in results between columns are a finding; the absence of such differences is equally a finding.

Each directory contains:

* `tls-lib-simple.pvl`: The cryptographic library and protocol definitions.
* `tls13-multiagent.pv`: The network topology and multi-agent replication execution.
* `queries.pvl`: The phase-structured correspondence queries.
* `sanity.pvl`: Reachability and dead-code checks.
* `verification_results.txt`: The raw compilation outputs.

---

## Running the Models

From the relevant subdirectory:

```bash
proverif205 -lib tls-lib-simple.pvl -lib sanity.pvl -lib queries.pvl -html traces tls13-multiagent.pv 2>&1 | tee log-variant.txt

```

---

## Test Case: CVE-2026-33697

To establish a verified baseline, all four models are evaluated against a known, real-world vulnerability: the attestation binding flaw identified in **CVE-2026-33697**.

The vulnerability is a relay attack on intra-handshake attestation. In the flawed protocol, the attestation nonce (`rdata`) is computed as `hash(pubEK, ar)` — binding Evidence only to the server's ephemeral encapsulation key and the client's attestation nonce. The handshake transcript (`log_SH`), the server's long-term identity (`pubLTK`), and the key exchange shares are entirely absent from this computation. This decoupling makes valid Evidence portable: an attacker can present genuine Evidence from one session as valid in a different session, without holding any session-specific key material. The flaw is present identically in both the DHE and KEM-based protocol variants, because the attestation binding is independent of the key exchange primitive.

The mitigated protocol (`./fix/`, `pq-kem/fix/`) closes this path using a two-layer HKDF binder derived from the handshake transcript, combined with an RFC 9345 Delegated Credential construction that cryptographically commits the Evidence to the specific session and the server's long-term identity simultaneously.

---

## Threat Model and System Architecture

This analysis operates strictly within the **Dolev-Yao threat model**, the standard abstraction for symbolic verification tools like ProVerif. Under this model, the adversary has complete control over the public network — they can intercept, modify, replay, and inject messages — but cannot break cryptographic primitives mathematically.

### Multi-Agent Topology

The system model utilizes a multi-tenant cloud architecture. The model allows for multiple concurrent client and server sessions. To rigorously capture the asymmetric nature of KEMs, the model replaces symmetric DH equations with directional encapsulation (`kemEncaps`) and decapsulation (`kemDecaps`), ensuring only the holder of the corresponding private key can extract the shared secret.

### Cryptographic Failure Modes

The model explicitly evaluates the protocol against granular key compromise scenarios to determine exactly which keys are required to execute a relay or forgery attack:

* **LeakedAK**: Compromise of the Attestation Key.
* **LeakedEK**: Compromise of the Endorsement Key (VM Identity).
* **LeakedLTK**: Compromise of the Long-Term Identity Key.

---

## Query Structure

Each `queries.pvl` file is organized into lettered sections, each targeting a distinct layer of the protocol's security surface. The queries organized per verification target are structured as follows:

* **Part A — DH/KEM Identity:** Tests whether the client's view of the session key can be traced to genuine server participation. This is the relay attack at the primitive layer, independent of attestation.
* **Part B — Binding Level Analysis:** A progressive sweep across Evidence binding properties at two protocol checkpoints (Level 2: handshake traffic keys; Level 3: application traffic keys). Each property is tested first without escape conditions, then with progressively combined key compromise scenarios, to identify the minimal sufficient condition set required for security to hold.
* **Part C — Phase-Structured Attack Surface Analysis:** Nine queries organized across three protocol checkpoints — Phase 1 (Evidence Origin & Transcript Binding at `log_SH`), Phase 2 (Full Session Composition at `log_SFIN`), Phase 3 (End-to-End Application Data). Each phase is tested against three compromise combinations, establishing which attack conditions are necessary and sufficient at each depth.
* **Part D — One-Way Agreement Baseline:** Tests server aliveness and one-way agreement properties (non-injective, injective, and injective with nonces) under the full combined escape set.
* **Part E — Progressive Composition Binding:** Tests the `ClientComp`/`PreServerComp` correspondence events, which carry parameters from both the RA and TLS layers simultaneously, confirming that the RA-to-TLS composition binding holds under the same conditions as the individual layers.
* **Parts F & G — LTK Assumption Analysis:** Isolates the role of the long-term identity key across all layers, testing whether LTK alone, LTK+AK, LTK+EK, and LTK+AK+EK are individually sufficient or insufficient attack conditions at the Evidence, session, composition, and application data layers.
* **Sanity checks (`sanity.pvl`):** Reachability queries confirming the model reaches all expected protocol states, plus co-occurrence checks verifying that paired client/server events can occur in the same trace. Results annotated `EXPECTED true` in the source reflect structurally intentional properties — specifically, that the relay attack breaks mutual identity agreement at every level of agreement granularity, which is itself a finding rather than a modeling limitation.

---

## Verification Outcomes: DHE vs. PQ-KEM Parity

Reading across the 2×2 matrix, the results demonstrate strict, one-to-one structural parity between the idealized DHE and idealized KEM columns:

1. **Vulnerability Reproduction (CVE row):** Every attack path present in the idealized DHE CVE model reproduces cleanly in the idealized KEM CVE model. In both, neither LeakedAK alone nor LeakedEK alone is sufficient to bypass Level 2 binding; the joint compromise of both is required. The composition layer fails with identical logic across both primitives.
2. **Mitigation Parity (Fix row):** The idealized DHE and idealized KEM fix models match on every query. The Delegated Credential binder closes the EK relay path uniformly across both primitives. In both, two independent sufficient attack conditions are established: LeakedAK alone, or the joint compromise of LeakedLTK and LeakedEK.
3. **Primitive-Level Deltas:** The only deviations reflect expected, structurally necessary differences between the abstractions. To maintain structural symmetry with the DHE model's weak subgroup attacks (`SentBadElement`, `ServerChoosesKEX(WeakDH,...)`), the idealized KEM models deliberately abstract a weak KEM failure state (`SentBrokenKEMSecret`, `ServerChoosesKEX(KEM_13(BadCiphertext))`). The session binding value is updated to `kem_ss` in place of `gxy`. No security-relevant result flips between columns.

---

## Methodological Scope and Limitations

- **Standalone Scope:** This repository evaluates the transition from standalone DHE to standalone ML-KEM. It does not currently model a hybrid key exchange (e.g., X25519+MLKEM768). Extending `tls-lib-simple.pvl` to support a concatenated hybrid key schedule is a welcome avenue for future contribution.

- **Side-Channel Leakage:** Symbolic verification via ProVerif treats cryptographic algorithms as perfect black boxes. Physical implementation vulnerabilities, execution timing, and hardware-level side-channel leakage cannot be evaluated through this methodology and require distinct computational or physical analysis frameworks.

---


## Copyright and License

Copyright 2017 Karthikeyan Bhargavan, Bruno Blanchet, and Nadim Kobeissi.
Copyright 2025 Muhammad Usama Sardar, Mariam Moustafa, and Tuomas Aura.
Copyright 2026 Nathanael Ritz.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

## Acknowledgements

This work is a unique adaptation and extension, developed apart from the original
academic model released under the Apache 2.0 license:

[CCC-Attestation repository](https://github.com/CCC-Attestation/formal-spec-id-crisis/tree/main)

Original TLS 1.3 library model produced by Bhargavan et al. is available
at: [reftls](https://github.com/Inria-Prosecco/reftls/blob/master/pv/tls-lib.pvl)
