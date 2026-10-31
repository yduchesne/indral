# Indral — Learning resources mapped to the product roadmap

**Curated:** 2026-10-31 · **Status:** Learning guide, not an implementation specification.  
**Roadmap:** [Phases 1–8](../roadmap/ROADMAP.md) · **Initial focus:** Phases 1–3 (domain-independent Core), followed by Phase 4 (Manufacturing). Phase 5 (Smart Buildings) is an independent, optional domain. Phases 7–8 (Quervant and AI) are deferred.

## How to use this guide

This is a practical curriculum for a software engineer learning industrial connectivity, MES/MOM, BAS, industrial reliability, and temporal operations intelligence. **Prioritize courses, demos, and small local labs over reading entire protocol specifications.** Each entry describes the topic and its application to Indral. Study only the topics needed for the next deliverable; don't block Phase 1 on optional Phase 5–8 training.

**Cost labels:** **Free** = instructional content is publicly available; **Free account** = no-cost registration may be needed; **Free docs / paid software** = tutorials are readable but products/modules/lab licensing may cost; **Partial free / paid course** = a trial or introductory module is free; **Usage charges** = cloud or metered services can incur charges. Fees, course catalogues, URLs and access conditions can change. **Do not interpret a free tutorial as a free certification exam, software license, or AWS sandbox.** No resource listed is a dependency on buying third-party software.

**Recommended learning method:** Watch/read the topic → complete a small guided exercise → implement a deterministic local Indral fixture → write failure-mode and end-to-end tests → demonstrate the result.

## At a glance

| Phase | Main subjects | Start here |
|---|---|---|
| **1 — Connectivity** | OT networking; Modbus TCP, OPC UA, MQTT, BACnet/IP; basic asset identity; Ignition | Cisco OT Fundamentals; Inductive University; OPC UA Connect; BACnet Institute |
| **2 — Operational Data** | SCADA, historian, alarm/event models, quality, reliability, PostgreSQL, htmx/ECharts | Inductive University historian/alarming; PostgreSQL; htmx examples |
| **3 — Temporal Intelligence** | Valid/knowledge time, corrections, graph, incident timelines, provenance | Martin Fowler bitemporal history; PostgreSQL ranges; W3C PROV |
| **4 — Manufacturing** | MES/MOM, ISA-95, production, OEE, six big losses, genealogy, quality, CMMS | Sepasoft MES courses/tutorials; ISA-95 free module; Vorne OEE |
| **5 — Smart Buildings (optional)** | BAS/HVAC, equipment/zone semantics, Brick/Haystack, energy | BACnet Institute; Brick; Project Haystack |
| **6 — Reliability and Deployment** | OT security, recovery, observability, edge-to-AWS | CISA/INL free ICS courses; NIST OT security; AWS Greengrass |
| **7 — Quervant (deferred)** | Native graph, ontology inference, indexed retrieval, provenance consistency | Quervant design documents |
| **8 — Agentic AI (deferred)** | Bedrock, AgentCore, LangGraph, Strands evaluation and LLM evaluation | AWS exam plan; LangChain Academy; AgentCore tutorials |

---

## Phase 1 — Industrial connectivity and operational modeling (Indral Core)

**Outcome:** All four read-oriented protocol adapters feed a domain-neutral source/asset model. Ignition is an **optional external system**.

### OT fundamentals, ISA-95 boundaries, Ignition

| Resource and access | Description / what to practice |
|---|---|
| [Cisco U. — Introduction to OT and ICS Fundamentals](https://u.cisco.com/courses/introduction-ot-ics-fundamentals-28213) — Free course | OT vs IT, industrial network architecture, ICS components, Purdue layers and segmentation. Good starting point before protocol and network testing. |
| [Inductive University](https://inductiveuniversity.com/) — Free courses / account | Hands-on Ignition gateways, OPC connections, tags, device connectivity and diagnostics. Study the Gateway, OPC UA and Tags units before attempting interoperability. |
| [ISA — ISA-95 overview and free introduction](https://www.isa.org/standards-and-publications/isa-standards/isa-95-standard) — Free intro; full standard/training may cost | Understand enterprise/control boundaries, physical vs logical manufacturing equipment, production hierarchy and manufacturing information exchange. **Do not** hardcode ISA-95 into Core. |
| [Cisco Networking Academy](https://www.netacad.com/) — Free and paid learning paths | Networking fundamentals (routing, switching, VLANs, subnetting). A targeted refresher for BACnet/IP broadcast and segmented plant-network scenarios. |

### Modbus TCP

| Resource and access | Description / what to practice |
|---|---|
| [PyModbus documentation and tutorials](https://www.pymodbus.com/docs) — Free | Python client/server examples, register and coil read operations, decoding, timeouts and error responses. Build a deterministic simulator and **read-only** client. |
| [Modbus Organization — specifications](https://www.modbus.org/specs.php) — Free reference | Application protocol and Modbus/TCP detail; use for register/addressing, exception codes and conformance tests after completing a tutorial. |

### OPC UA

| Resource and access | Description / what to practice |
|---|---|
| [OPC UA Connect — Free Academy](https://opcuaconnect.com/en/learn/) — Free lessons; free account for video/labs | Structured foundations/build tracks covering address spaces, sessions, browse, data values, subscriptions and security. No physical PLC needed. |
| [OPC UA Connect — Write a Client and Server](https://opcuaconnect.com/en/learn/build/write-a-client-and-a-server/) — Free guided course | Practical client/server tasks including a Python asyncua path; learn enough to design a robust adapter without treating protocol semantics as generic telemetry alone. |
| [FreeOpcUa asyncua examples](https://github.com/FreeOpcUa/opcua-asyncio/tree/master/examples) — Free open-source examples | Minimal Python server/client, subscriptions, status and source/server timestamps. Excellent reproducible fixture for CI. |
| [Unified Automation — OPC UA webinar recordings](https://www.unified-automation.com/services/training/ua-webinar.html) — Free recorded webinars | Additional introductions to OPC UA information modeling, sessions, security and client/server interoperability. |

### MQTT

| Resource and access | Description / what to practice |
|---|---|
| [HiveMQ — MQTT Essentials](https://www.hivemq.com/mqtt/) — Free tutorial series | Topics, QoS, retained messages, sessions, reconnects and Will messages. Learn why transport delivery guarantees do not establish evidence completeness. |
| [EMQX — MQTT Guide](https://www.emqx.com/en/mqtt-guide) — Free articles and tutorials | Python clients, MQTT 5, brokers and topic modeling; run the examples against a **local test broker**. |
| [Eclipse Mosquitto documentation](https://mosquitto.org/documentation/) — Free docs | Broker configuration and diagnostics for isolated MQTT tests. Prefer this to using a publicly writable broker for Indral fixtures. |

### BACnet/IP

| Resource and access | Description / what to practice |
|---|---|
| [BACnet Institute — BACnet Basics, Device Profiles](https://thebacnetinstitute.org/courses-overview/) — Free account and courses | Learn devices, object/property models, services, conformance profiles and interoperability. Ideal before implementing discovery, reads and COV. |
| [BACnet Institute — Resource Library](https://thebacnetinstitute.org/resources-overview/) — Free account | Technical presentations on discovery, networks, troubleshooting, interoperability and cybersecurity. |
| [BAC0 Python — Getting Started](https://bac0.readthedocs.io/en/latest/getstarted.html) — Free guided examples | Practical BACnet/IP discovery, device interaction and property reads. Uses BACpypes3; a useful candidate for fixture/protocol-library evaluation, **not** a locked technology choice. |
| [BACnet Committee — FAQ](https://bacnet.org/faq/) — Free reference | Terminology and implementation context after the introductory course. |

**Indral exercise:** Run one synthetic source for each protocol. Capture native locator, canonical asset ID, value, quality and timestamp provenance. Deliberately omit one source timestamp; interrupt/reconnect all sources; use both BACnet discovery and explicitly configured known-device access. Confirm no write commands are exposed.

---

## Phase 2 — Operational data platform (Indral Core)

**Outcome:** PostgreSQL historian, generic events/alarms, source-health monitoring and FastAPI/Jinja2/htmx/ECharts UI.

### SCADA, historian and alarms

| Resource and access | Description / what to practice |
|---|---|
| [Inductive University](https://inductiveuniversity.com/) — Free courses | Take the **Tag Historian, Alarming, Database, Tag and Gateway** lessons. Study deadbands, quality, alarm lifecycle, history and store-and-forward. |
| [Ignition — Alarm study guide](https://training.inductiveautomation.com/core-certification/study-guide/topics-covered/alarming/) — Free study material | Alarm detection, acknowledgments, journaling and notifications. Separate device connection errors from process alarms. |
| [Sepasoft — MES training videos](https://www.sepasoft.com/video-library/) — Free video library | Preview machine states, OEE inputs and production dashboards; contextual learning **only**—no MES rules in Core. |

### Time-series, integration reliability and UI

| Resource and access | Description / what to practice |
|---|---|
| [PostgreSQL — Date/Time Functions](https://www.postgresql.org/docs/current/functions-datetime.html) — Free reference | Time zones, timestamp arithmetic, interval grouping and source/persisted timestamp handling. |
| [PostgreSQL — Table Partitioning](https://www.postgresql.org/docs/current/ddl-partitioning.html) — Free reference | Partitioning strategies and operational tradeoffs for large append-heavy historian tables. No forced partition design at this stage. |
| [AWS Prescriptive Guidance — Transactional Outbox](https://docs.aws.amazon.com/prescriptive-guidance/latest/cloud-design-patterns/transactional-outbox.html) — Free architectural tutorial | Understand dual-write failures, durable propagation and idempotent downstream consumers; applicable locally without AWS service dependency. |
| [htmx — Examples](https://htmx.org/examples/) — Free hands-on UI examples | Incremental server-rendered status panels, polling, validation and partial updates with minimal JavaScript. |
| [Apache ECharts — Getting Started](https://echarts.apache.org/handbook/en/get-started/) — Free tutorial | Timeline, historian trend and alarm visualization; practice zoom, missing samples and status indicators. |
| [Grafana — Learning Hub](https://grafana.com/docs/learning-hub/) — Free learning resources; hosted features may cost | Optional supplemental exercises in telemetry, metrics, logs and incident investigations, not a replacement for Indral UI. |

**Indral exercise:** Build a generic equipment/connection dashboard, historian plots, event/alarm journal and a diagnostic panel across all four protocols. Inject duplicate samples, a missing interval, an out-of-order event and a restart. Do not silently interpolate gaps or invent source timestamps.

---

## Phase 3 — Temporal intelligence and Operational Time Travel (Indral Core)

**Outcome:** Bitemporal entities/relationships, historic graph, evidence provenance, deterministic incident timeline and time (T, K) reconstruction.

### Temporal modeling

| Resource and access | Description / what to practice |
|---|---|
| [Martin Fowler — Bitemporal History](https://martinfowler.com/articles/bitemporal-history.html) — Free illustrated article | **Start here:** separates when a fact applied from when a system learned/recorded it, including late corrections and two-time queries. |
| [PostgreSQL — Range Types](https://www.postgresql.org/docs/current/rangetypes.html) — Free reference | Valid-time and knowledge-time intervals, overlaps, constraints and indexing for versioned asset edges. Not a complete bitemporal implementation by itself. |
| [PostgreSQL — WITH / Recursive Queries](https://www.postgresql.org/docs/current/queries-with.html) — Free reference | Deterministic graph traversals and their limitations; useful for temporal relationship discovery before Quervant exists. |

### Evidence provenance and interactive graph

| Resource and access | Description / what to practice |
|---|---|
| [W3C — PROV Primer](https://www.w3.org/TR/prov-primer/) — Free illustrated primer | Evidence sources, derivations, transformations, agents and activities. Learn its vocabulary without introducing an RDF dependency. |
| [Cytoscape.js — Docs and demos](https://js.cytoscape.org/) — Free library tutorials | Render historical relationships, highlighted paths and changes over selected time windows. |
| [Apache ECharts — Handbook](https://echarts.apache.org/handbook/en/get-started/) — Free examples | Synchronize incident timelines with graph selection, alarms and late-arrival markers. |
| [Event Sourcing — Martin Fowler](https://martinfowler.com/eaaDev/EventSourcing.html) — Free architecture article | Compare immutable event logs/replay with bitemporal historical state; related concepts that are **not interchangeable**. |

**Indral exercise:** A measurement valid at 09:58 arrives at 11:30. At operational time T=10:00, compare knowledge cutoff K=10:10 with K=12:00; add a retroactive relationship correction and prove neither destroys what was previously recorded. Distinguish Indral's recorded knowledge from actual operator awareness.

---

## Phase 4 — Manufacturing domain: MES, MOM and CMMS

**Outcome:** Production orders/execution, OEE/downtime, quality, batch/material genealogy, MES and CMMS interoperability, manufacturing investigation.

### ISA-95 and practical MES foundations

| Resource and access | Description / what to practice |
|---|---|
| [ISA — ISA-95 free overview module](https://www.isa.org/standards-and-publications/isa-standards/isa-95-standard) — Free overview; full program/standards may cost | Manufacturing hierarchy, operations models and ERP/MES/SCADA boundaries. Domain semantics belong in **Manufacturing**, not Indral Core. |
| [Sepasoft — MES Course Library](https://www.sepasoft.com/courses1/) — **Free online courses** | Highest-priority hands-on learning: **MES Basics**, **OEE Downtime**, **Settings & Changeover**, **Business Connector**, **Web Services**. |
| [Sepasoft — MES Video Library](https://www.sepasoft.com/video-library/) — Free short lessons | MES architecture, OEE, batch recipes, track-and-trace, quality and integration demonstrations. Good to watch even without installing modules. |
| [Sepasoft — Module Tutorials](https://docs.sepasoft.com/articles/mes-module-tutorials/training-materials) — Free documentation; MES product modules may need paid licensing | Step-by-step **OEE Downtime, SPC, Track and Trace, Batch Procedures, ERP Connectivity**. Use as workflow reference; do not require Sepasoft in Indral runtime. |
| [Sepasoft — Learn / Getting Started Webinars](https://www.sepasoft.com/learn/) — Free webinars | Demonstrates setup, first production run, database integration and basic production dashboard in a real MES environment. |

### OEE, downtime and production losses

| Resource and access | Description / what to practice |
|---|---|
| [Vorne — Practical OEE](https://www.oee.com/practical-oee/) — Free illustrated guide | Availability × Performance × Quality, planned production time, cycle time and counting rules. Turn formulas into deterministic tests. |
| [Vorne — Six Big Losses](https://www.vorne.com/learn/tools/six-big-losses/) — Free illustrated learning guide | Planned/unplanned stops, minor stops, reduced speed, startup rejects and production defects: realistic fault scenarios for the simulator. |

### Genealogy, quality, CMMS and enterprise integration

| Resource and access | Description / what to practice |
|---|---|
| [Sepasoft Track & Trace, Batch, SPC and ERP Tutorials](https://docs.sepasoft.com/articles/mes-module-tutorials/training-materials) — Free reading; licensed exercises may cost | Model lot consumption and production genealogy, quality deviations, batch steps, ERP-to-MES message boundaries and connector failure handling. |
| [NIST/SEMATECH Engineering Statistics Handbook](https://www.nist.gov/programs-projects/nistsematech-engineering-statistics-handbook) — Free handbook | Statistical process control and variation; distinguish quality measurements from automatically established causal explanations. |
| [Fiix — Maintenance blog and CMMS resources](https://fiixsoftware.com/blog/) — Free practical articles; product may cost | Reactive vs preventive maintenance, work-order lifecycles, asset hierarchy and CMMS integration vocabulary. |
| [MESA International](https://mesa.org/) — Free public articles; courses/membership may cost | Vendor-neutral Manufacturing Operations Management perspective and industry use cases. Optional breadth resource after Sepasoft. |

**Indral exercise:** Simulated bottling/packaging line with production order, materials, good/reject counts, downtime, fault and external CMMS work order. Compute OEE and genealogy deterministically; investigate the production interruption via Core T/K reconstruction. Do not build an ERP, scheduler or full MES.

---

## Phase 5 — Smart Buildings/BAS domain (**optional; independent of Manufacturing**)

**Outcome:** Distinct building-owned equipment/zone/occupancy/energy model using existing Core connectivity, historian and temporal services. **BACnet support already exists in Phase 1; no HVAC model is required in Core.**

### BAS/HVAC and facility operations

| Resource and access | Description / what to practice |
|---|---|
| [BACnet Institute — Facility Manager's Guide to BAS](https://thebacnetinstitute.org/courses-overview/) — Free account/course | BAS design, procurement, operation, commissioning and typical system boundaries; strong industry-oriented overview. |
| [BACnet Institute — BACnet Cybersecurity](https://thebacnetinstitute.org/courses-overview/) — Free account/course | BACnet/SC and building OT security; learn future interoperability constraints without making BACnet/SC a Core Phase 1 dependency. |
| [ASHRAE eLearning](https://www.ashrae.org/professional-development/learning-portal) — Mixed availability; many paid courses | Optional deeper HVAC, controls and energy training if free BACnet/BAS instruction is insufficient. Check current course offerings and costs. |

### Building data semantics and energy

| Resource and access | Description / what to practice |
|---|---|
| [Brick Schema — Documentation](https://docs.brickschema.org/) — Free examples and reference | Buildings, spaces, equipment, points and relationship semantics. Source for **building-domain** vocabulary, not a Core ontology mandate. |
| [Project Haystack — Introduction](https://www.project-haystack.org/doc/docHaystack/Intro) — Free tutorial/reference | Tags, site/space/equipment/point concepts and typed data APIs for building metadata integration. |
| [Project Haystack — Ontology](https://www.project-haystack.org/doc/docHaystack/Ontology) — Free reference | Semantic definitions, subtype relationships, units and entity relationships. Compare with Brick when modeling devices/points. |
| [DOE Better Buildings — Resources](https://betterbuildingssolutioncenter.energy.gov/resources) — Free public guidance and webinars | Building energy use, benchmarking and operational improvement. Supplemental business-domain context, not a required Indral dependency. |

**Indral exercise:** Build a small **separate** BAS/HVAC fixture (one AHU and two zones), map synthetic BACnet points into building-owned entities, reconstruct a zone-comfort incident. Prove no changes to Core historian/temporal invariants are required.

---

## Phase 6 — Security, reliability and local/AWS deployment

**Outcome:** Secure, reproducible local deployment and AWS deployment support without exposing industrial endpoints to the public internet.

### OT/ICS security and operational resilience

| Resource and access | Description / what to practice |
|---|---|
| [CISA / Idaho National Laboratory — ICS Cybersecurity Training](https://inl.gov/national-security/ics-cybersecurity-training/) — **Free self-paced courses; registration** | ICS/OT components, deployment differences, risks, attacks and IT/OT defensive practices. Prioritize deployment and defense modules; online units are often ~1 hour. |
| [NIST SP 800-82 Rev. 3 — Guide to OT Security](https://csrc.nist.gov/pubs/sp/800/82/r3/final) — Free security reference | OT segmentation, inventory, incident response, safety/availability tradeoffs, remote access and defense in depth. Reference after hands-on CISA lessons. |
| [BACnet Institute — Cybersecurity course](https://thebacnetinstitute.org/courses-overview/) — Free account/course | Security posture of BACnet/BACnet/SC, especially the risks of unsegmented discovery and legacy device connectivity. |
| [OpenTelemetry — Documentation](https://opentelemetry.io/docs/) — Free tutorials | Tracing, metrics and logging across adapters, ingestion, historian and API. Correlate operational failures without leaking credentials. |
| [PostgreSQL — Backup and Restore](https://www.postgresql.org/docs/current/backup.html) — Free tutorials/reference | Restore exercises and history preservation; backups should cover evidence, provenance and timeline invariants. |

### AWS edge/cloud integration and portability

| Resource and access | Description / what to practice |
|---|---|
| [AWS IoT Greengrass V2 — Getting Started](https://docs.aws.amazon.com/greengrass/v2/developerguide/getting-started.html) — Free documentation; **AWS usage charges may apply** | Build and deploy a small edge component, then evaluate secure forwarding from a plant-local collector to AWS. Optional; no Greengrass requirement. |
| [AWS IoT Greengrass V2 — Tutorials](https://docs.aws.amazon.com/greengrass/v2/developerguide/tutorials.html) — Free tutorials; **usage charges may apply** | MQTT edge interaction, component rollout and secure device operations. Use V2; V1 is past end of support. |
| [AWS IoT SiteWise — Documentation](https://docs.aws.amazon.com/iot-sitewise/latest/userguide/what-is-sitewise.html) — Free docs; **usage charges may apply** | Compare AWS asset/time-series models with Indral's canonical equipment model. Optional interoperability/managed-service research. |
| [AWS Well-Architected — Reliability Pillar](https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/welcome.html) — Free reference | Availability, error recovery, observability and failure testing; apply selectively to Indral's local/cloud deployment. |

**Indral exercise:** Simulate gateway loss, reconnect, backlog and database recovery; verify no silent history loss. Deploy Core + Manufacturing to local and AWS environments with equivalent API/investigation tests. Industrial protocol adapters should remain near industrial devices or simulated edge endpoints.

---

## Phase 7 — Quervant search and ontology (**deferred**)

| Resource and access | Description / what to practice |
|---|---|
| [Quervant — Repository](https://github.com/yduchesne/quervant) — Project docs | Review the actual, current implementation; do not infer that approved future plans are shipped capabilities. |
| [Quervant — Ontology Specification Index](https://github.com/yduchesne/quervant/blob/main/docs/ontology/README.md) — Free project design | Read approved semantic model and the distinction between approved conceptual design and proposed extensions. |
| [Quervant — QOS-001](https://github.com/yduchesne/quervant/blob/main/docs/ontology/QOS-001.md) — Free project design | Class membership, typed asserted relationships, constraints and snapshot semantics. |
| [Quervant — QOS-002](https://github.com/yduchesne/quervant/blob/main/docs/ontology/QOS-002.md) — Free project design | Declarative archetypes and bounded inference. General-purpose engine semantics—not hardcoded ISA-95 or BAS logic. |
| [Quervant — Graph roadmap](https://github.com/yduchesne/quervant/blob/main/docs/graph/ROADMAP.md) — Free project design | Track native graph feature maturity before designing an integration requiring graph traversal/inference. |

**Indral exercise (only after Quervant is ready):** Index versioned asset/event/maintenance projections; verify search freshness and bitemporal consistency against PostgreSQL. Failure of Quervant must not disable authoritative Core reconstruction.

---

## Phase 8 — Agentic industrial investigations (**deferred until non-agentic functionality is complete**)

| Resource and access | Description / what to practice |
|---|---|
| [AWS Certified Generative AI Developer – Professional](https://aws.amazon.com/certification/certified-generative-ai-developer-professional/) — Free exam guide/prep overview; **exam and some labs paid** | Exam domains, AWS service requirements and recommended Skill Builder plan; ties agentic work to the certification learning objective. |
| [AWS Skill Builder](https://skillbuilder.aws/) — Free digital courses + optional paid labs/subscription | Bedrock, IAM, model integration, RAG and evaluation. Enroll only after selecting the specific training needed for agent integration. |
| [LangChain Academy](https://academy.langchain.com/) — **Free course content; optional paid certification** | LangGraph state, durable agent workflows, tool calling and LangSmith evaluation/observability. |
| [Amazon Bedrock AgentCore — Getting Started](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/agentcore-get-started-cli.html) — Free tutorial; **AWS usage charges may apply** | Build, test and deploy a code-based agent with tools. Distinguish AgentCore runtime/hosting from LangGraph orchestration. |
| [AgentCore — On-demand Evaluations](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/getting-started-on-demand.html) — Free tutorial; **AWS usage charges may apply** | Evaluation workflows and instrumentation, useful for checking sourced findings and unsupported causal claims. |
| [Strands Agents — Documentation](https://strandsagents.com/latest/) — Free framework docs; **model calls may cost** | Evaluate as an alternative or complement to LangGraph only when there is a concrete design reason. Not an initial dependency. |

**Indral exercise:** Create a read-only investigator that calls deterministic Core tools, supplies source evidence for every finding and refuses unsupported causal certainty. Compare answers against fixed non-agentic investigation fixtures; Quervant is optional.

---

## Choosing a cost-effective learning strategy

- **Best return for the first two phases:** Inductive University, PyModbus, OPC UA Connect, HiveMQ MQTT Essentials, BACnet Institute, htmx examples, PostgreSQL and ECharts. No commercial MES license required.
- **Best MES learning for Phase 4:** Sepasoft's free course library and module videos combined with Vorne's OEE/Six Big Losses. Use the simulated MES/CMMS integrations to avoid license requirements.
- **Only pay for something after a gap is proven:** a particular simulator, a formal credential, a lab product, or a training module that cannot be reproduced with free fixtures.
- **Do not start AWS or AI metered exercises unintentionally:** establish sandbox budgets and teardown procedures before launching cloud resources.
- **Treat all third-party material as educational input:** verify semantics and licensing before using example code; follow Indral's own [architecture boundaries](../architecture/CORE_BOUNDARIES.md), [connectivity contract](../architecture/CONNECTIVITY.md), and [Core acceptance criteria](../roadmap/CORE_ACCEPTANCE.md).

## Updating this resource list

For each proposed new resource, record: roadmap phase/topic, direct URL, type (course/lab/tutorial/reference), access/cost conditions, a one-sentence learning outcome, and an Indral exercise it supports. Prefer provider-owned materials and stable project docs. Revalidate URLs and fees periodically; archive or replace inaccessible or discontinued courses. Do not silently change product scope based on a training provider's feature set.
