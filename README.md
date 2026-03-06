# Formal analysis of attested TLS protocols

Sardar and collaborators provided a formal proof of insecurity of two protocols using state-of-the-art tool [ProVerif](https://ieeexplore.ieee.org/document/9833653) and released the models to the open source community, dubbed "Identity Crisis in Confidential Computing". This specific work is a unique adaptation and extension, developed apart from the original academic model released under the Apache 2.0 license: [https://github.com/CCC-Attestation/formal-spec-id-crisis/tree/main](https://github.com/CCC-Attestation/formal-spec-id-crisis/tree/main)

This repository contains further formalizations of other intra-handshake attestation proposals demonstrating mitigation of the disclosed attacks.

## Main results

- Intel's RA-TLS/Interoperable RA-TLS is vulnerable to replay attacks.
- Intel's RA-TLS/Interoperable RA-TLS and draft-fossati-tls-attestation are both vulnerable to diversion attacks.
- *Formalization of a cryptographic binder in fossati-seat-early-attestation-03 [Early] demonstrates mitigation of both replay and diversion attacks.

| Property                   	       | IRA-TLS| TLS-a | *Early |
| :--                		             | :--    | :--   | :-- |
| G-RA1: Integrity of Evidence       | ✅     | ✅    |✅    | 
| G-RA2: Freshness of Evidence       | ❌     | ✅    |✅    |
| G-RA3: Secrecy of Attestation Keys | ✅     | ✅    |✅    |
| G-TLS1: Server Identity            | ❌     | ❌    |✅    |
| G-TLS2: Server Authentication      | ❌     | ❌    |✅    |
| G-C1: Compound Authentication      | ❌     | ❌    |✅    |
| G-C2: Agreement of All Parameters  | ❌     | ❌    |✅    |


## Tool 
### Installing ProVerif
Install the latest version (2.05 at the moment) of ProVerif: see https://bblanche.gitlabpages.inria.fr/proverif/ for details.
See Section 1.4 of [manual](https://bblanche.gitlabpages.inria.fr/proverif/manual.pdf) for installation options:
- via OPAM: Section 1.4.1
- from sources: Section 1.4.2
- from binaries: Section 1.4.3 

## Artifacts organization
- Folder `fossati-seat-early-attestation-03` contains code for newly proposed I-D for TLS-attest protocol with mitigations against replay and diversion attacks.
- Folder `TLS-a` contains code for original TLS-attest standard candidate.
- Folder `TLS-a/fix` contains code for proposed fix for TLS-attest standard candidate.

```text
formal-spec-id-crisis/
│
├── README.md                          # README file
│
│
├─ fossati-seat-early-attestation-03/  # Newly proposed I-D for TLS-attest protocol with cryptographic binder
│     ├── tls-lib-simple.pvl           # ProVerif library file
│     ├── tls13-multiagent.pv          # ProVerif main file
│     ├── README.md                    # Folder-specific README.md outlining specific changes implemented to the original formalization
│ 
├── TLS-a/                             # Original TLS-attest protocol (draft-fossati-tls-attestation)
      ├── tls-lib-simple.pvl           # ProVerif library file
      ├── tls13-multiagent.pv          # ProVerif main file
      │
      ├── fix/                         # Proposed fix by original academic authors for TLS-attest protocol (draft-fossati-tls-attestation)
           ├── tls-lib-simple.pvl      # ProVerif library file
           ├── tls13-multiagent.pv     # ProVerif main file
```

## Running automatic proofs 

### Basic Execution
Run as follows: 

```bash 
proverif -lib tls-lib-simple.pvl tls13-multiagent.pv
```

### Generation of traces for failing properties
In order to additionally generate a trace for each property which results in "false", create a subfolder (e.g., `traces` in the following command) for results before executing.

```bash 
mkdir traces
```

Then to execute: run as follows:
```bash 
proverif -lib tls-lib-simple.pvl -graph traces tls13-multiagent.pv
```

OR 
```bash 
proverif -lib tls-lib-simple.pvl -html traces tls13-multiagent.pv
```

Subfolder `traces` will contain the traces in .dot as well as .PDF.

### Saving log
To additionally save in log file together with display:
```bash
proverif -lib tls-lib-simple.pvl -html traces tls13-multiagent.pv 2>&1 | tee log.txt
```

### Horn clauses
To additionally see the Horn clauses generated in ProVerif: 

a. use command-line option `-test` as follows: 
```bash
proverif -lib tls-lib-simple.pvl tls13-multiagent.pv -test
```

OR 

b. add one of the following two settings inside the input (*.pv) file:

- `set verboseClauses = short.` to display the Horn clauses

- `set verboseClauses = explained.` to additionally display a sentence after each clause it generates to explain where this clause comes from.

### Interactive mode
To run in interactive mode:
```bash
proverif_interact -lib tls-lib-simple.pvl tls13-multiagent.pv
```

<!---
#❓
--->

## Original Artifacts author
Muhammad Usama Sardar (contact: muhammad_usama.sardar at tu-dresden.de)

## Pre-print
Preprint is available [here](https://www.researchgate.net/publication/398839141_Identity_Crisis_in_Confidential_Computing_Formal_Analysis_of_Attested_TLS).

## Scientific Publication
The work is accepted for publication at AsiaCCS and should be cited as follows: 

> Muhammad Usama Sardar, Mariam Moustafa, and Tuomas Aura. 2026.
Identity Crisis in Confidential Computing: Formal Analysis of Attested
TLS. In ACM Asia Conference on Computer and Communications Security
(ASIA CCS ’26), June 1–5, 2026, Bangalore, India. ACM, New York, NY, USA,
14 pages. https://doi.org/10.1145/3779208.3785387

BibTeX:
```
@inproceedings{Sardar2026IdCrisis,
address = {New York, NY, USA},
author = {Sardar, Muhammad Usama and Moustafa, Mariam and Aura, Tuomas},
booktitle = {Proceedings of the 21st ACM ASIA Conference on Computer and Communications Security (ACM ASIACCS 2026)},
publisher = {ACM},
title = {{Identity Crisis in Confidential Computing: Formal Analysis of Attested TLS}},
doi={10.1145/3779208.3785387},
year = {2026}
}
```

## Acknowledgments
- Ionut Mihalcea 
- Jean-Marie Jacquet
- Thomas Fossati
- Eric Rescorla
- Hannes Tschofenig
- Yaron Sheffer
- Laurence Lundblade
- Giridhar Mandyam
- Christopher Patton
- Jonathan Hoyland
- Richard Barnes

Several others at the IETF, IRTF and CCC have contributed by providing feedback.

