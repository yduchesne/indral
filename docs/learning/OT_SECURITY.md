# OT Security learning track for Indral

**Updated:** 2026-10-31 · **Status:** Curated training and practice guide; not an implementation specification.  
**Navigation:** [Complete phase-by-phase learning catalogue](RESOURCES.md) · [Roadmap](../roadmap/ROADMAP.md) · [Core connectivity](../architecture/CONNECTIVITY.md)

## Objective and boundaries

Learn to build and assess an industrial connectivity and intelligence platform that preserves **safety, availability, trusted evidence and read-only operation** across Modbus TCP, OPC UA, MQTT and BACnet/IP. The goal is **OT-specific engineering and integration competence**, not a second general IT security curriculum. Security is **cross-cutting from Phase 1**; Phase 6 hardens and validates the whole system.

**Lab safety rule:** All demonstrations, packet analysis, discovery and security validation must target **owned, isolated simulators or explicitly authorized lab environments**. Do not run broad discovery, penetration testing, exploit demonstrations, aggressive probes or active vulnerability scanning against production controllers, BAS devices, third-party networks or safety systems. Prefer passive capture and offline PCAP analysis. Never test device writes or control commands against real equipment.

**Cost labels:** **Free** content; **Free account** may require registration; **Free preview / paid training** indicates only an introductory module is free; **Free resource / eligibility** may limit who can register; **Optional commercial** means useful but not necessary. These labels describe training content, not certification exams or commercial licenses.

## Recommended learning sequence

| Sequence | Topics | Apply in phase | Indral deliverable |
|---|---|---|---|
| **A — OT threat and safety model** | IT vs OT, cyber-physical consequences, Purdue/segmentation, asset inventory | 1 | Threat model and read-only network topology for four adapters |
| **B — Protocol-specific security** | Modbus/BACnet trust limits, OPC UA certificates/PKI, MQTT broker ACL/TLS | 1–2 | Capability constraints, protocol identity and security-focused negative tests |
| **C — Detection and forensic evidence** | OT traffic, ATT&CK for ICS, passive monitoring, event quality and provenance | 2–3 | Safe network captures, alert/event timelines and defensible evidence |
| **D — OT risk, requirements and response** | IEC 62443 zones/conduits, security levels, supply chain, incident handling | 4–6 | Risk register, architecture review, tabletop exercise and control mapping |
| **E — Deployment security** | Edge boundaries, credentials, backups, auditability, secure remote access | 6 | Verified local/AWS deployment controls and recovery tests |

## A. Foundations: OT networks, safety and threat modeling

| Resource & access | Brief description / practice |
|---|---|
| [CISA/INL — ICS Cybersecurity Training catalogue](https://inl.gov/national-security/ics-cybersecurity-training/) — **Free, registration** | **Primary starting course series.** Includes short Virtual Learning Portal courses: ICS Cybersecurity Practices **100W**, component/deployment modules **210W-01–04**, risk/threat/consequence modules **210W-05–08**, attack methodologies **210W-09**, and defense-in-depth **210W-10/11**. Focus on what makes OT different from traditional enterprise security. |
| [CISA/INL — ICS Cybersecurity (300)](https://inl.gov/national-security/ics-cybersecurity-training/) — **Free, registration** | More substantial **12–15 hour virtual course** with structured labs on ICS environments, discovery/mapping, network defense and analysis. Take after the 100W/210W foundation and **use only the provided lab**. |
| [TryHackMe — Introduction to the World of OT/ICS](https://tryhackme.com/room/introductiontotheworldofotics) — **Account, free-room availability should be checked** | Beginner-friendly guided overview of PLCs, HMIs, SCADA, industrial processes and operator/safety considerations. Optional quick on-ramp for unfamiliar plant terminology; check access level before enrolling. |
| [NIST SP 800-82 Rev. 3 — Guide to OT Security](https://csrc.nist.gov/pubs/sp/800/82/r3/final) — **Free reference** | Broad, authoritative architecture guidance for OT environments: risks, control selection, segmentation, remote access, availability and security/operations tradeoffs. Focus on architecture and operational constraints, not memorizing the full document. |
| [CISA and partners — Foundations for OT Cybersecurity: Asset Inventory](https://www.cisa.gov/sites/default/files/2025-08/joint-guide-foundations-for-OT-cybersecurity-asset-inventory-guidance_508c.pdf) — **Free guide** | Build an inventory of operational assets, dependencies, criticality and ownership. Translate into Indral's source identity, native locator, connection metadata and graph provenance contracts. |
| [Joint government guidance — Principles of Operational Technology Cyber Security](https://www.ic3.gov/CSA/2024/241001.pdf) — **Free guide** | Six principles encompassing physical consequence, operations knowledge, OT data value, segmentation, supply chains and personnel; a practical short architectural checklist. |

**Lab A:** Draw the network zones for simulated plant devices, local OT data collectors, historian, application, operator UI and optional cloud services. Identify failure and trust boundaries. Record controls that prevent discovery and data flows from traversing unintended segments.

## B. ISA/IEC 62443 architecture and security requirements

| Resource & access | Brief description / practice |
|---|---|
| [ISA — IEC 62443 Cybersecurity Certificate Program](https://www.isa.org/certification/certificate-programs/isa-iec-62443-cybersecurity-certificate-program) — **First module free; remaining modules/exams paid** | Start with **IC32M01, Introduction to Control Systems Security**. Free preview modules also exist for risk assessment (IC33), design (IC34) and maintenance (IC37). Do **not** label the whole course free. |
| [ISA — Self-paced modular training](https://programs.isa.org/free-training) — **Free first modules; paid full programs** | An alternative direct starting point for IC32, plus optional SCADA integration module IC30. Understand the **zones/conduits** perspective and technical vs organizational control requirements. |
| [CISA — CSET (Cyber Security Evaluation Tool)](https://github.com/cisagov/cset) — **Free tool / documentation** | Interactive IT/OT assessment workflows, security architecture/network diagram and control gap reporting. Evaluate Indral's *synthetic* site without exposing a real plant; note Windows requirements for some packages. |
| [CISA — Assessment Evaluation and Standardization (AES) courses](https://www.cisa.gov/resources-tools/programs/assessment-evaluation-and-standardization-program) — **Course access may require registration/eligibility** | The CSET course and Cybersecurity Performance Goals 2.0 course cover structured assessment and baseline controls. Confirm access details; use the materials for a small evidence-driven control review. |
| [CISA/NSA partners — Secure by Demand OT product-selection guide](https://www.fbi.gov/file-repository/cyber-alerts/secure-by-demand-priority-considerations-for-operational-technology-owners-and-operators-when-selecting-digital-products-011325.pdf/view) — **Free guide** | Questions OT buyers should ask about secure-by-design products, identity, configurations and lifecycle. Turn the guide into review questions for Indral's simulator, gateway and adapter choices. |

**Lab B:** Produce an **Indral OT security requirements matrix**: zones/conduits, identity and trust, secure configuration, monitoring, availability, recovery, logging, maintenance and secure remote administration. Separate implemented controls from planned ones; do not self-certify IEC 62443 conformance.

## C. Protocol-specific security, lab troubleshooting and PKI

| Resource & access | Brief description / practice |
|---|---|
| [OPC UA Connect — Security and PKI](https://opcuaconnect.com/en/learn/build/security-and-pki/) — **Free lessons; labs require free account** | **Especially recommended.** ~96-minute course on Sign vs SignAndEncrypt, certificate identities/SANs, trust/rejected lists, identity tokens, roles, revocation and certificate lifecycle. Exercises use example servers; prefer a locally owned fixture for CI and failure injection. |
| [OPC Foundation — UA Part 2: Security Model](https://reference.opcfoundation.org/specs/OPC-10000-2/1) — **Free specification/reference** | Foundation for endpoint policies, application/user authentication, auditing, secure channels and availability. Consult when writing OPC UA adapter negative tests and support matrix. |
| [HiveMQ — MQTT Essentials](https://www.hivemq.com/mqtt/) — **Free tutorials** | Learn broker sessions, delivery semantics and network behavior; extend with **TLS, broker-side authentication and topic-scoped authorization** using local broker documentation. QoS does **not** mean authenticity or evidence completeness. |
| [Mosquitto — Documentation](https://mosquitto.org/documentation/) — **Free broker docs** | Configure an isolated broker with explicit accounts/ACLs, local TLS and restricted subscriptions; test rejection of unauthorized topics and invalid certificates. No cloud broker needed. |
| [BACnet Institute — BACnet Cybersecurity course](https://thebacnetinstitute.org/courses-overview/) — **Free account/course** | Understand BACnet/IP security limits and BACnet/SC, trust and building-network considerations. **BACnet/SC remains beyond Phase 1 adapter scope**; the course informs later hardening. |
| [Wireshark — Display Filters](https://wiki.wireshark.org/DisplayFilters) and [Modbus reference](https://www.wireshark.org/docs/dfref/m/modbus.html) — **Free tutorial/reference** | Safely read packet captures from local fixtures, identify expected protocol requests/replies and model network baselines. Capture only traffic you own; never assume a dissector proves authenticity. |

**Lab C:** In containers/isolated VMs, compare successful vs rejected OPC UA certificate handshakes; reject unauthorized MQTT topic access; verify Modbus and BACnet adapters expose **only read-side capabilities**, enforce configured peer lists and do not silently scan networks. Produce local PCAPs for debugging.

## D. Detection engineering, adversary behavior and evidence

| Resource & access | Brief description / practice |
|---|---|
| [MITRE ATT&CK for ICS — Matrix](https://attack.mitre.org/matrices/ics/) — **Free knowledge base** | OT threat techniques including discovery, loss of view/control and alarm suppression. Use as a vocabulary for **defensive detection hypotheses**, not an instruction to perform attacks on real devices. |
| [MITRE ATT&CK Data & Tools](https://attack.mitre.org/resources/attack-data-and-tools/) — **Free datasets** | ICS mappings, mitigations and relationships; useful for controlled examples and documenting detection-to-technique coverage. |
| [SANS — Automating the ICS 5 Critical Controls for Free](https://www.sans.org/presentations/automating-the-sans-ics-5-critical-controls-for-free) — **Free summit presentation/material** | OT-specific defense priorities and practical approaches. Compare monitoring, access control and recovery controls with a small simulator deployment. |
| [Dragos OT-CERT](https://www.dragos.com/community/ot-cert) — **Free community resources; membership may require eligibility/registration** | OT asset/risk toolkits, workshops, logging and incident-response guidance. **Dragos Academy's broader commercial platform training is not assumed free.** |
| [SANS — ICS/OT Incident Response guide](https://www.sans.org/posters/industrial-control-system-cyber-incident-response) — **Free downloadable poster** | Safe cyber position, preparation, operators/engineering responsibilities, containment, evidence preservation and recovery. Useful tabletop reference. |

**Lab D:** Create **synthetic** suspicious-activity indicators (unusual read-rate, failed authentication, unexpectedly new connection, stale telemetry, changed asset binding) in Indral's own fixtures. Record what was actually observed, detection time, source reliability, and whether the event was visible to a hypothetical operator. Use operational time T and knowledge cutoff K to reconstruct the incident without manufacturing false causation claims. Do not generate real attack traffic.

## E. OT incident response, maintenance and deployment hardening

| Resource & access | Brief description / practice |
|---|---|
| [CISA/INL — ICS training workshops and assessment modules](https://inl.gov/national-security/ics-cybersecurity-training/) — **No tuition; registration/availability constraints** | Continue with defense and risk-assessment materials. In-person workshops have different enrollment/travel requirements; focus on the no-cost online courses first. |
| [Dragos OT-CERT — practical program resources](https://www.dragos.com/blog/ot-cybersecurity-best-practices-for-smbs-managing-default-passwords-and-identifying-ics-ot-devices-exposed-to-the-internet/) — **Free public articles; member toolkits** | Inventory, backups, secure remote access, security logging, ransomware tabletop drills and incident-handling checklists for smaller OT operators. |
| [SANS — ICS/OT Incident Response guide](https://www.sans.org/posters/industrial-control-system-cyber-incident-response) — **Free** | Safely coordinate technical response with equipment owners and plant personnel. Define preservation/rollback expectations before connectivity changes. |
| [PostgreSQL — Backup and Restore](https://www.postgresql.org/docs/current/backup.html) — **Free docs** | Verify full recovery of asset/evidence/version histories, including valid time, knowledge time, mapping history and incident records. |
| [NIST SP 800-82 Rev. 3](https://csrc.nist.gov/pubs/sp/800/82/r3/final) — **Free** | Revisit remote access, least privilege, monitoring, legacy-device risk, vulnerability/patch windows and change management during deployment design. |

**Lab E:** Run an incident-response tabletop: a simulated OT gateway becomes untrusted, ingestion stops, a certificate expires, then an offline buffer arrives late. Verify source status transitions, prevention of unsafe reconnection, preserved evidence, authenticated recovery, delayed-event semantics and documented operator handoff.

## Suggested course path (high-value, free/low-cost first)

1. **CISA/INL 100W + 210W-01–11** — OT environment, risk and defense basics.
2. **ISA IC32M01 free module** — IEC 62443 security lifecycle and zones/conduits.
3. **OPC UA Connect Security and PKI** — immediately applicable to the Phase 1 adapter.
4. **BACnet Institute Cybersecurity** + **Mosquitto TLS/ACL exercises** — protocol-specific boundaries.
5. **CISA/INL ICS Cybersecurity (300)** — longer online guided exercises, within the provider's lab.
6. **MITRE ATT&CK for ICS + SANS incident-response materials** — defensive hypotheses and evidence.
7. **CSET synthetic-site assessment + Dragos OT-CERT** — operational security review and deployment checklist.

If time is limited, prioritize **1, 2, 3, 4** during Phase 1 and **5–7** across Phases 2–6. Given an existing cybersecurity background, focus on the **OT-specific consequences and constraints** instead of retaking general CISSP-level coverage.

## How this track maps onto Indral acceptance criteria

| Phase | Security acceptance additions or emphasis |
|---|---|
| **1** | Document adapter threat model; explicit read-only capability sets; no secrets in logs; source authenticity/trust metadata; bounded discovery; safe local topology; OPC UA certificate validation. |
| **2** | Authenticated data paths and UI; role-limited operational access; health and audit events; defensive controls for malformed payloads, replay and out-of-order telemetry; persisted evidence with timestamps. |
| **3** | Historical corrections and late evidence never erase the earlier knowledge state; provenance and access-controlled investigation trails; uncertainty/completeness signaled. |
| **4** | MES/CMMS connector identities and permissions; protect production, maintenance and quality records from untrusted external updates; log mapping/correction provenance. |
| **5 (optional)** | BAS-specific hardening, BACnet boundary review and building operational risks; **no BAS concepts in Core**. |
| **6** | OT network segmentation, credential rotation, local/AWS secure forwarding, monitoring, recovery and tabletop test evidence. |
| **7–8 (deferred)** | Search projection ACL/provenance enforcement, AI tool-level authorization and safe read-only agent behavior; no control authority inferred from integration availability. |

**No new mandatory implementation scope is approved by this guide.** New acceptance tests and controls should be specified in a dedicated design PR in accordance with Core's read-only, domain-independent architecture. This document makes the required OT-security *learning* more concrete; it is not an IEC 62443 compliance claim.

## Maintenance and access caveats

External course access, registration eligibility, prices and schedules change. Confirm links and registration terms before enrolling. Provider-managed labs, particularly those involving offensive techniques, must be used solely as authorized exercises; outside that environment, stick to local, isolated and consented test fixtures.
