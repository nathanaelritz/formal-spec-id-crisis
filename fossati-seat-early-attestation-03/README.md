# Early Attestation Model

ProVerif model for [draft-fossati-seat-early-attestation-03](https://datatracker.ietf.org/doc/draft-fossati-seat-early-attestation/), adapted from the [TLS-a](https://github.com/CCC-Attestation/formal-spec-id-crisis/tree/main/TLS-a) model by Sardar, Moustafa, and Aura.

This model is intended as a faithful formalization of the Early Attestation binder mechanism, with minimal changes beyond those required to encode the draft.

## What this model proves

Injective compound agreement over `(ID_S, pubEK, psk, offer, mode, kc, ks, ems, rms, cr, sr, dev_state)` holds unless both `privAK` and `privEK` are simultaneously compromised:

```
inj-event(ClientComp(...)) ==> inj-event(PreServerComp(...)) || LeakedEK(pubEK)   — true
inj-event(ClientComp(...)) ==> inj-event(PreServerComp(...)) || LeakedAK(pubAK)   — true
inj-event(ClientComp(...)) ==> inj-event(PreServerComp(...))                      — false
```

The third result (false) confirms the boundary is not vacuous.

## Modeling assumptions

**Adversary capability** is active and standard: the adversary controls the network and may selectively compromise keys via `LAK` (leak `privAK`) and `LEK` (leak `privEK`). Platform measurements are adversary-supplied (`in(io, dev_status1: bitstring)`), so the adversary may instantiate any TEE state; only a TEE presenting `dev_statusRef` will be accepted at the client.

**Weak DH and hash exclusions** are preserved from the original TLS-a queries. The sanity and agreement queries are conditioned on `ServerChoosesKEX ≠ WeakDH` and `ServerChoosesHash ≠ WeakHash`, consistent with the original model's treatment of algorithm agility.

**Certificate verification**: the client verifies the CA signature over `(ID_S, pubEK_S)` before accepting evidence. The original TLS-a client does not perform this check; it is added here to match the Early Attestation draft's WebPKI integration.

**EncryptedExtensions** is modeled as a transcript-contributing message (`out(io, EE(EExts))` on the server, received and incorporated into `log_EE` on the client).

## Key differences from the original TLS-a model

| Aspect | Original | This model |
|---|---|---|
| Binding mechanism | `hash(pubEK)` + standalone nonce | transcript-derived `s_attest_binder` |
| EncryptedExtensions in transcript | omitted | included |
| CA cert verification by client | no | yes |
| Evidence encryption | no | no |
| Weak DH/hash exclusions in queries | yes | yes |
| Adversary-chosen measurements | yes | yes |
| Multi-agent topology | yes | yes |


Expected runtime is approx 5 minutes on Apple M2 with 16 GB of memory.
