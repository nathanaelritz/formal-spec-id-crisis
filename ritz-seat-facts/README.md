# FACTS Model

This model is a work in progress to support the [FACTS over TLS 1.3](https://datatracker.ietf.org/doc/draft-ritz-seat-facts/) IETF I-D and has not been independently peer-reviewed. Operating in some part as a superset of the [fossati-seat-early-attestation-03](https://github.com/nathanaelritz/formal-spec-id-crisis/tree/main/fossati-seat-early-attestation-03) (aka Early Attestation) model, FACTS introduces a third factor, `privKEM`, for HPKE-based nonce encapsulation that enables the conveyance of encrypted evidence, and post-handshake application data verification. The model is split into modular compilation units to support concurrent ProVerif runs to decrease verification times using Docker containers.

## What this model demonstrates

Every property follows a three-pillar structure: agreement holds as long as any single key among `privTIK`, `privKEM`, and `privAK` remains uncompromised. Each property includes a falsification boundary (bare query, no leak assumption) that must return false to confirm non-vacuity.

**Compound agreement** over `(ID_S, pubTIK, psk, offer, mode, kc, ks, ems, rms, cr, sr, pubKEM, dev_state)`:

```
inj-event(ClientComp(...)) ==> inj-event(PreServerComp(...)) || LeakedTIK(pubTIK)   — true
inj-event(ClientComp(...)) ==> inj-event(PreServerComp(...)) || LeakedKEM(pubKEM)   — true
inj-event(ClientComp(...)) ==> inj-event(PreServerComp(...)) || LeakedAK(pubAK)     — true
inj-event(ClientComp(...)) ==> inj-event(PreServerComp(...))                        — false
```

**Post-handshake application data** (EKU compound): injective correspondence of both the compound handshake and the post-rotation app data exchange, under each single-key pillar independently.

Full query definitions and expected results are documented in each query file under `queries/`.

## Key differences from the Early Attestation model

| Aspect | Early Attestation | FACTS |
|---|---|---|
| Key architecture | 2 keys (AK, EK) | 3 keys (AK, TIK, KEM) |
| Nonce binding | transcript-derived binder | dual-nonce HPKE challenge + binder |
| Evidence confidentiality | plaintext | sealed under `attest_psk` |
| Post-handshake app data | not modeled | `eku_sts = hkdf_extract(ms, attest_psk)` |
| Pre-handshake discovery | not modeled | identity document over `untrusted_dns` |
| DH / hash negotiation | modeled (WeakDH/WeakHash) | hardcoded StrongDH/StrongHash |
| Platform measurements | adversary-chosen | hardcoded to `dev_statusRef` |
| Query structure | `{AK, EK, sanity}` triples | `{TIK, KEM, AK, falsification}` quads |
| File structure | 2 files | 15 files (modular compilation) |
| Verification strategy | single run (~5 min) | 3-way concurrent split (~55 min each) |

## Modeling assumptions

**Adversary capability** is active. The adversary controls the network and may selectively compromise keys via `LAK` (leak `privAK`), `LTIK` (leak `privTIK`), and `LKEM` (leak `privKEM`). Pre-handshake identity document discovery occurs over `untrusted_dns`, an adversary-observable channel; the client verifies the CA signature before trusting any fetched key material.

**Ideal cryptography**: `StrongDH` and `StrongHash` are hardcoded in the process bodies. This eliminates weak-algorithm disjuncts from all queries as a deliberate measure to control state explosion. The model does not claim immunity from poor cryptographic choices; it operates under typical TLS 1.3 cryptographic assumptions.

**Platform measurements** are hardcoded to `dev_statusRef`. Every CVM runs identical firmware, removing adversary-chosen measurement instantiation as a source of state space growth. The client still checks `dev_status1 = dev_statusRef`.

**Certificate verification**: the client verifies the CA signature over `(ID_S, pubTIK, pubKEM)` before the handshake begins, via the pre-handshake identity document. The server performs a self-check against the same cert before accepting sessions.

**WithAK / WithKEM event families**: parallel events that bind `pubAK` or `pubKEM` directly into the event term close the universally-quantified gap that would otherwise allow a leak assumption to match any key in the system rather than the session-specific one.

**Lemmas**: two ProVerif lemmas assist solver convergence. The first links `attest_psk` secrecy to `privKEM` compromise; the second links `privKEM` knowledge to the `LeakedKEM` event.

## File structure

```
tls-lib-simple-queryless.pvl    Base TLS 1.3 primitives and key schedule (no queries)
facts-lib.pvl                   FACTS-specific types, functions, events, tables
facts-handshake.pvl             FactsClient and FactsServer process definitions
facts-entrypoint.pv             Agent generation, topology, main process, run commands

queries/
  lemmas.pvl                    Solver-assist lemmas
  key-leaks.pvl                 Reachability sanity checks for leak events
  key-secrecy.pvl               privAK / privTIK / privKEM secrecy
  traffic-key-secrecy.pvl       Application write key (kc) secrecy
  G-TLS1.pvl                    Server identity binding
  G-TLS2a.pvl                   Aliveness
  G-TLS2d.pvl                   Recent one-way injective agreement
  G-CA1.pvl                     Compound authentication with full identity
  G-C2.pvl                      Compound injective agreement
  G-RA.pvl                      RA integrity and per-session freshness
  eku-compound.pvl              Post-rotation app data + eku_sts/attest_psk secrecy
```

## Running the model

Expected runtime is approx 55 minutes per partition on Apple M2 with 16 GB of memory. The three partitions (TLS, RA, EKU) can be run concurrently. Suggested run commands are found directly in `facts-entrypoint.pv`.

For Docker setup and build instructions, see the [root README](../../README.md).

### TLS partition

```bash
rm -R ./traces/tls; mkdir -p ./traces/tls
docker run --rm -v "$(pwd)":/work proverif205 -lib work/tls-lib-simple-queryless.pvl -lib work/facts-lib.pvl -lib work/facts-handshake.pvl -lib work/queries/lemmas.pvl -lib work/queries/key-leaks.pvl -lib work/queries/key-secrecy.pvl -lib work/queries/traffic-key-secrecy.pvl -lib work/queries/G-TLS1.pvl -lib work/queries/G-TLS2a.pvl -lib work/queries/G-TLS2d.pvl -html work/traces/tls work/facts-entrypoint.pv 2>&1 | tee tls-log.txt
```

### RA partition

```bash
rm -R ./traces/ra; mkdir -p ./traces/ra
docker run --rm -v "$(pwd)":/work proverif205 -lib work/tls-lib-simple-queryless.pvl -lib work/facts-lib.pvl -lib work/facts-handshake.pvl -lib work/queries/lemmas.pvl -lib work/queries/key-leaks.pvl -lib work/queries/G-CA1.pvl -lib work/queries/G-C2.pvl -lib work/queries/G-RA.pvl -html work/traces/ra work/facts-entrypoint.pv 2>&1 | tee ra-log.txt
```

### EKU partition

```bash
rm -R ./traces/eku; mkdir -p ./traces/eku
docker run --rm -v "$(pwd)":/work proverif205 -lib work/tls-lib-simple-queryless.pvl -lib work/facts-lib.pvl -lib work/facts-handshake.pvl -lib work/queries/lemmas.pvl -lib work/queries/key-leaks.pvl -lib work/queries/eku-compound.pvl -html work/traces/eku work/facts-entrypoint.pv 2>&1 | tee eku-log.txt
```
