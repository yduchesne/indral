# Indral

Domain-independent industrial intelligence platform supporting Modbus, OPC UA, MQTT, and BACnet, with temporal graphs, bitemporal history, and Operational Time Travel.

> **Status:** Planning/architecture. Capabilities documented below are proposed, **not yet implemented**.

Indral Core (Phases 1–3) provides protocol connectivity, historian and operational data services, and a bitemporal investigation graph. Manufacturing/MES (Phase 4) and Smart Buildings/BAS (Phase 5, optional) are separate domain applications built on the same core. Ignition is an optional external integration. PostgreSQL is authoritative; Quervant and agentic AI are later, non-blocking extensions.

## Documentation

- [Documentation index](docs/README.md)
- [Product scope and exclusions](docs/PRODUCT.md)
- [Architecture and core/domain boundaries](docs/architecture/CORE_BOUNDARIES.md)
- [Connectivity contracts (Modbus, OPC UA, MQTT, BACnet)](docs/architecture/CONNECTIVITY.md)
- [Temporal model and Operational Time Travel](docs/architecture/TEMPORAL_MODEL.md)
- [Overall roadmap](docs/roadmap/ROADMAP.md)
- [Core acceptance criteria](docs/roadmap/CORE_ACCEPTANCE.md)

Indral is designed for local-first, read-only-by-default operation. Implementation work begins after the foundational architecture has been reviewed and detailed Phase 1 contracts are specified.
