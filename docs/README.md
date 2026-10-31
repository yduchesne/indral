# Indral documentation

**Status: Under development.** This repository currently contains product decisions and planning documents. Described capabilities are **not yet implemented or production-ready**.

## Getting started

- [Project README](../README.md) — short product description, project status and entry points.
- [Product definition and scope](PRODUCT.md) — goals and exclusions.
- [Overall roadmap and dependencies](roadmap/ROADMAP.md) — Phases 1–8, including independent domain applications.
- [Learning resources and practical exercises](learning/RESOURCES.md) — curated free/affordable courses, tutorials and reference material for every roadmap topic.

## Architecture and validation

- [Core architecture and domain boundaries](architecture/CORE_BOUNDARIES.md)
- [Four-protocol connectivity design](architecture/CONNECTIVITY.md)
- [Temporal model and Operational Time Travel](architecture/TEMPORAL_MODEL.md)
- [Reference scenarios and validation](architecture/REFERENCE_SCENARIOS.md)
- [Core Phase 1–3 acceptance plan](roadmap/CORE_ACCEPTANCE.md)
- [ADR-0001 — Foundational architecture](decisions/ADR-0001-foundation.md)

## Reading rules

1. A **decision** records the current product planning baseline; an **implementation specification** must refine interfaces, storage schemas and protocol details before coding.
2. A **phase** is a product outcome, **not** permission to defer tests, security or basic recovery until a later phase.
3. **Core (Phases 1–3)** remains domain-independent. Manufacturing/MES (Phase 4) and optional Smart Buildings/BAS (Phase 5) own their specific semantics.
4. **Modbus, OPC UA, MQTT and BACnet connectivity** are Core features; support does not imply active control or every profile of each protocol.
5. **Quervant and AI are not dependencies** of any Core or Manufacturing feature.
6. Course materials are educational references, not tool/library selections or product dependencies.

Architectural scope changes should update the roadmap and an ADR.
