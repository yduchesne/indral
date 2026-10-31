# Temporal intelligence and Operational Time Travel

**Status:** Contractual invariants for Phase 1–3 design; exact schema and query execution plan are deferred.

## Why this is Core, not MES

Equipment topology, operational events, measurements, delayed evidence and incident investigation appear in factories, commercial buildings, utilities and other OT environments. Temporal history is **independent of the operational domain**.

## Temporal axes and data fidelity

- **Valid time:** the interval at which an asset property, state or relationship is asserted to apply in the modeled operational world. It is not necessarily the time a packet arrived.
- **Knowledge/recorded time:** when Indral's authoritative store accepted the assertion, correction or supersession. It must never be silently backdated.
- **Source event/measurement time:** the time asserted by the device or upstream system, when available. Source clocks can be wrong or missing.
- **Received time:** when Indral's adapter/gateway first obtained the message.
- **Persisted time:** when an authoritative record was committed. For knowledge-time queries this must be tied to a well-defined durable commit/order boundary.
- **Operator awareness:** distinct from Indral knowledge. It can only be reconstructed when notification, visibility and acknowledgment evidence is actually available.

Do not conflate timestamps or infer valid time uncritically from source time. A timestamp's provenance and trust classification are part of its evidence.

## Historical reconstruction contract

Core exposes a logical inquiry:

> Reconstruct entities, relationships, state and evidence valid at operational time **T**, using information durably known to Indral by **K**.

A query must include: T, K, domain filter/context where provided, evidence references, completeness/warning indicators and the query's consistent knowledge snapshot. Show differences between two knowledge cutoffs, including late arrival and retroactive corrections.

The time selected for a measurement query may be a window, not a single instant. Incidents require explicit time-zone, interval boundary and clock-skew policies in the concrete spec.

## Core graph behavior

- Canonical entities and typed edges have stable identity and history, not just current snapshots.
- Store topology additions, deletions, reassignments, type changes and corrected relationships without erasing prior recorded assertions.
- Permit domain relationship labels as data but keep graph storage/traversal generic.
- No inference of causality from graph adjacency or correlated timestamps alone.
- Persist supporting source IDs, records, import mappings, validity basis and correction lineage.
- Query handling must never return a misleading "not present" result when data is incomplete, invalid or query budget is exhausted.

## Illustrative scenario

09:58 a vibration anomaly occurs; 10:02 a pump fault is logged; 10:06 a production delay occurs; 11:30 a disconnected gateway delivers buffered 09:58 measurements.

- T=10:00, K=10:10: reconstructed evidence must exclude the buffered reading not yet recorded.
- T=10:00, K=12:00: the reading may now support a retrospective anomaly analysis.
- Neither view proves the pump **caused** the production delay merely because timestamps and graph links overlap.

To claim what the human operator knew at 10:00, the record would additionally need system-display/delivery evidence.

## Phase sequencing

- **Phase 1:** canonical IDs; source identity; timestamp/quality fields; mapping provenance; immutable reference evidence conventions.
- **Phase 2:** durable historian, event/alarm log, reliable intake, retention policies that do not erase required reconstruction history.
- **Phase 3:** bitemporal tables, correction semantics, versioned relations, reconstruction engine, evidence views, Cytoscape.js graph and ECharts timelines.
- **Phases 4–5:** domain-specific relationship types, incidents and derived analytics consume these services.

## Deferred to detailed design

Exact table/index/partition layout; clock synchronization policy; graph traversal budget; delete/retention contracts; event identity/dedup keys; snapshot transaction model; storage cost controls; proof of consistency under re-ingestion; temporal query syntax/API; provenance serialization. Decisions must come with deterministic test fixtures.
