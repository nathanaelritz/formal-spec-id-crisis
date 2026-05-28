# Formal Analysis: TLS + RA + ML-KEM

This repository contains ProVerif formal verification models and query results comparing the baseline Cocos AI intra-handshake attestation implementation (CVE-2026-33697) against a mitigated design based on draft-fossati-seat-early-attestation-04 and an RFC 9345 Delegated Credential construction.

Two model variants are provided:

- **DHKE** — classical Diffie-Hellman key exchange
- **ML-KEM** — asymmetric KEM abstraction replacing the DH commutativity equations, reflecting draft-ietf-tls-mlkem-07

Each variant includes a flawed (CVE) model and a mitigated model, with paired query files.

## Running the Models

From the relevant subdirectory:

```bash
proverif205 -lib tls-lib-simple.pvl -lib sanity.pvl -lib queries.pvl -html traces tls13-multiagent.pv 2>&1 | tee log-mlkem.txt
```

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

## Disclaimers

This work is a unique adaptation and extension, developed apart from the original
academic model released under the Apache 2.0 license:

https://github.com/CCC-Attestation/formal-spec-id-crisis/tree/main

Original TLS 1.3 library model produced by Bhargavan et al. is available
at: https://github.com/Inria-Prosecco/reftls/blob/master/pv/tls-lib.pvl
