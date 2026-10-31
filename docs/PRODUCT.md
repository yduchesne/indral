# Product definition and scope

## Repository description

> Domain-independent industrial intelligence platform supporting Modbus, OPC UA, MQTT, and BACnet, with temporal graphs, bitemporal history, and Operational Time Travel.

## Purpose

Indral connects to operational technology, collects and preserves signals and events, and reconstructs what happened across equipment, relationships, and systems — including the difference between **when a fact applied** and **when Indral learned it**.

It is not primarily a SCADA replacement, a commercial MES, or a building automation controller. Its distinguishing user workflow is **deterministic, evidence-backed historical investigation**.

## Product organization

- **Indral Core (Phases 1–3):** generic protocol connectivity; asset/source identity and typed relationships; telemetry/historian; state/event/alarm handling; temporal graph; evidence provenance; historical investigation API and generic UI.
- **Manufacturing (Phase 4):** ISA-95-informed entities, production orders and execution, OEE/downtime, quality, materials/batches, traceability, MES/CMMS integration and manufacturing investigations.
- **Smart Buildings (Phase 5; separately scheduled):** buildings/spaces/zones, BAS/HVAC/energy concepts, facilities maintenance, and building investigations. This is a distinct domain application, **not** part of Core.
- **Platform maturity (Phase 6):** hardening and local/AWS deployment parity for the completed target product. Basic security and recovery requirements apply from the first phase.
- **Future extensions (Phases 7–8):** Quervant retrieval/ontology integration and agentic investigations (Bedrock, AgentCore, LangGraph; Strands to evaluate).

Manufacturing is the first domain to implement. Smart Buildings is independently optional and **does not gate** Core, Manufacturing, platform hardening, or the future agentic track.

## Initial implementation constraints

- **Core protocol support:** Modbus TCP, OPC UA, MQTT and BACnet/IP as testable read-oriented adapters. Additional transport variants/profiles require separate decisions.
- **Data:** PostgreSQL is authoritative for operational and bitemporal history. Quervant is never required to preserve historical truth.
- **Web:** FastAPI, Jinja2, htmx, ECharts, Cytoscape.js; limited vanilla JavaScript for rich graphs/charts. **No React**.
- **Ignition:** external system for interoperability and learning; Indral works without it.
- **Local-first:** all Core and Manufacturing capabilities must work in local environments. AWS support is additive.
- **Deterministic-first:** complete the non-agentic platform before developing AI investigation features.
- **Safety:** read-only industrial connectivity by default. No write/control/actuation endpoints in initial Core scope.
- **Simulators:** reproducible test environments outside the Core business model; the first rich scenario is a simulated manufacturing line.

## Out of scope for the initial core

Manufacturing orders, OEE, batch genealogy, HVAC systems, building zones, occupancy comfort, ERP, advanced scheduling, active device control, automation optimization, domain-specific ontologies, full BACnet stack/network management, native Quervant graph/ontology requirements, and LLM agents.

## Outcomes to validate

1. Read telemetry and events from all four protocols via one coherent operational model **without discarding native protocol metadata**.
2. Query device health, assets, live measurements, alarms and stored history.
3. Reconstruct asset relationships and events at valid time T given knowledge available at time K.
4. Link investigation findings to persisted source evidence and distinguish observation, correlation and causal hypothesis.
5. Add Manufacturing and Smart Buildings as separate consumers without migrating domain assumptions out of Core.
