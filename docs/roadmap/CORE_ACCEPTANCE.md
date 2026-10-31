# Core Phases 1–3 — acceptance plan

**Purpose:** define falsifiable exit criteria and prevent generic-platform scope drift. This is **not yet** a detailed coding-agent instruction set.

## Shared quality gates (every phase)

- Repeatable setup, deterministic test fixtures and documented test commands.
- Unit, integration and end-to-end tests for each new vertical slice; security and fault cases relevant to that slice.
- Explicit schemas/contracts, migrations, API error responses and version compatibility expectations.
- Source provenance and quality retained wherever data is transformed.
- No uncontrolled device writes. No secret values in logs, traces, screenshots or example configurations.
- Human-verifiable local demonstration; do not claim completed functionality solely because docs describe it.

## Phase 1: protocol foundation

**Functional acceptance**
- [ ] Core asset identity and native source identity are stored distinctly, with configurable mappings.
- [ ] Modbus TCP acquisition works against a deterministic fixture, including decode and exception handling.
- [ ] OPC UA browse/read/subscribe works against a deterministic fixture; preserve NodeId, timestamps and status where provided.
- [ ] MQTT subscribe/decode works against a local broker and demonstrates expected QoS/reconnect behavior.
- [ ] BACnet/IP read/discovery works against a synthetic device, with known-device fallback and COV when fixture supports it.
- [ ] Each adapter exposes its actual capabilities, diagnostics and lifecycle states.
- [ ] Cross-adapter normalization does not invent time, engineering units or quality.
- [ ] No HVAC, production-order or business process types are required in Core.
- [ ] Ignition can exchange/observe planned data for supported interoperability paths, while Indral also starts without Ignition.

**Negative tests:** unreachable endpoints; malformed data; duplicate native names; corrupted payload; missing source timestamp; disconnect/reconnect; attempted unsupported write.

## Phase 2: operational platform

**Functional acceptance**
- [ ] Values, native source references, timestamps, quality and ingestion state persist to PostgreSQL.
- [ ] Historical query and trend view show data from all four adapters consistently.
- [ ] Generic events, alarms, acknowledgment state and device/connection health are queryable.
- [ ] FastAPI/Jinja2/htmx UI provides live/current asset views, alarms, history and operational status; ECharts powers timelines.
- [ ] Buffer/retry and dedup behavior is specified, exercised and observable; missing intervals are visible.
- [ ] No assumption that devices provide perfect clocks, ordered delivery or complete samples.

**Negative tests:** simulated outage, out-of-order observations, replay, database restart, inconsistent device/source status.

## Phase 3: temporal intelligence / Core completion

**Functional acceptance**
- [ ] Asset and relationship history persists valid-time and knowledge-time independently.
- [ ] Add, end, reassign and retroactively correct edges while preserving historical assertions.
- [ ] A reconstruction query accepts T (valid) and K (known); results identify query cutoffs and evidence references.
- [ ] Late delivery produces the expected difference between contemporaneous and retrospective knowledge states.
- [ ] Incidents combine asset relations, measurements, generic events and alarms into an evidence-backed timeline.
- [ ] Cytoscape.js displays the historical graph; ECharts displays temporal observations.
- [ ] Domain-neutral fixture is sufficient for full Core demonstration; no MES, BAS, Quervant or AI required.
- [ ] Unknown/incomplete results, source-clock uncertainty and query-budget failures are surfaced, not presented as definitive absence or causality.

**Negative tests:** retroactive correction; relationship reparenting; simultaneous competing assertions; incomplete event stream; no operator-awareness evidence; budget exhaustion.

## Exit rule

A phase is complete only after automated tests, reproducible documented local setup and a reviewer-verifiable demonstration succeed. Remaining constraints must be recorded as explicit limitations, not silently waived.

## Design-work still required

Protocol-specific Python library/version evaluation; authoritative source ID format; schema and partitioning; ingestion architecture; graph traversal interface; event/correction identity; time consistency and clock policy; test topology; app modularity; deployment. Separate design PRs must resolve these before implementation.
