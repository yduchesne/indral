# ADR-0001 — Core/domain separation and phased delivery

- **Status:** Accepted planning baseline (2026-10-31); subject to implementation design review
- **Decision owners:** Indral project
- **Applies to:** Product scope and Phase 1–8 dependencies

## Context

Indral began as an industrial integration and MES-adjacent investigation concept. Protocol reuse across manufacturing and building automation exposed a risk: the initial plan placed manufacturing execution in Core and delayed temporal intelligence until after the manufacturing domain. Both would distort a reusable platform.

## Decision

1. **Phases 1–3 produce a standalone Indral Core:** (1) generic connectivity and operational identities, (2) data/historian/events/alarms/UI, (3) bitemporal graph, provenance, incident timelines and Operational Time Travel.
2. **Manufacturing is Phase 4**, built as a domain application using Core; owns MES/MOM semantics, production orders, OEE, materials, quality, genealogy and MES/CMMS integrations.
3. **Smart Buildings is Phase 5**, a distinct optional domain application using Core; owns BAS/HVAC/energy/space semantics. It does not determine Core schemas and is not on the critical path for Manufacturing.
4. **Modbus, OPC UA, MQTT and BACnet connectivity are Core features** delivered through protocol adapters. BACnet/IP support does **not** imply an HVAC domain model in Core.
5. **PostgreSQL is the authoritative temporal store**, local functionality is mandatory, and Ignition is an external integration.
6. **Phase 6 matures the platform**, including AWS deployment, without deferring foundational security, tests, fault tolerance or backups.
7. **Quervant (Phase 7) and agentic AI (Phase 8) are later, optional independent extensions**, not dependencies of each other or Core. The non-agentic product must be complete before AI work starts.

## Consequences

- Positive: generic investigation functionality can be validated before MES; smart-building work can be independently scheduled; Quervant's maturity cannot block Indral.
- Costs: Core needs a meaningful domain-neutral fixture and disciplined adapter/time semantics; Manufacturing needs explicit mapping to the Core asset/event graph.
- Guardrail: do not introduce hypothetical plugin frameworks, broad ontology standards, or production control capabilities merely to support unimplemented future domains.

## Open implementation decisions (not decided here)

Library and version selection for each protocol; OPC UA security profile/conformance matrix; BACnet COV and network test topology; ingestion buffering technology; exact PostgreSQL partition strategy; graph query API; deployment orchestration and AWS service selections; multi-tenancy requirements; actual domain schema.
