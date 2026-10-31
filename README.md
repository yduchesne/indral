# Indral

**Domain-independent industrial intelligence platform supporting Modbus, OPC UA, MQTT, and BACnet, with temporal graphs, bitemporal history, and Operational Time Travel.**

> **Project status: Under development.** Indral is currently in the architecture and planning stages. The features described in this repository are intended capabilities; they are **not yet implemented or production-ready**.

Indral is a local-first, read-only-by-default platform for integrating operational systems, preserving equipment and event history, and reconstructing incidents across time, assets, and evidence.

**Indral Core (Phases 1–3)** provides multi-protocol connectivity, a PostgreSQL historian, operational events and alarms, bitemporal asset relationships, and historical investigation. **Manufacturing/MES (Phase 4)** is its first domain application. **Smart Buildings/BAS (Phase 5)** is a separate optional domain. PostgreSQL remains authoritative; Ignition is an optional external integration. Quervant and AI are later, non-blocking extensions.

## Documentation

| Document | Purpose |
|---|---|
| [Documentation index](docs/README.md) | Navigation and document conventions |
| [Product scope](docs/PRODUCT.md) | Product goals, boundaries, exclusions and technology decisions |
| [Overall roadmap](docs/roadmap/ROADMAP.md) | Phases 1–8, dependencies and milestones |
| [Learning resources by phase](docs/learning/RESOURCES.md) | Free/low-cost courses, tutorials and exercises for every roadmap phase |
| [OT Security learning track](docs/learning/OT_SECURITY.md) | CISA/INL training, IEC 62443, protocol security, detection, assessments and incident response |
| [Core acceptance criteria](docs/roadmap/CORE_ACCEPTANCE.md) | Testable completion gates for Phases 1–3 |
| [Core architecture and domain boundaries](docs/architecture/CORE_BOUNDARIES.md) | Core versus Manufacturing and Smart Buildings responsibilities |
| [Protocol connectivity design](docs/architecture/CONNECTIVITY.md) | Modbus TCP, OPC UA, MQTT, BACnet/IP and shared adapter contracts |
| [Bitemporal model and Operational Time Travel](docs/architecture/TEMPORAL_MODEL.md) | Valid/knowledge time, historical graph and provenance |
| [Reference scenarios](docs/architecture/REFERENCE_SCENARIOS.md) | Domain-neutral fixtures and future manufacturing/building demonstrations |
| [ADR-0001 — Foundation](docs/decisions/ADR-0001-foundation.md) | Formal baseline architectural decision and unresolved design items |

## Development approach

The **non-agentic platform comes first**: deliver and validate Core, then the Manufacturing domain, with optional Smart Buildings separately. Basic testing, security, evidence preservation and resilience apply from the start. Local operation is required; AWS deployment is a subsequent hardening milestone. The implementation will use FastAPI, Jinja2, htmx, ECharts and Cytoscape.js; **no React**.

No device write/control path is part of the initial protocol adapters. Implementation plans must refine the specifications before coding begins.
