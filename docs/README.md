# Indral documentation

**Status:** Foundational design baseline (proposed for review); no production implementation is implied.

## Starting points
- [Product definition and scope](PRODUCT.md)
- [Architecture and core/domain boundaries](architecture/CORE_BOUNDARIES.md)
- [Protocol connectivity contracts](architecture/CONNECTIVITY.md)
- [Temporal model and Operational Time Travel](architecture/TEMPORAL_MODEL.md)
- [Reference scenarios and validation](architecture/REFERENCE_SCENARIOS.md)
- [Overall roadmap and dependencies](roadmap/ROADMAP.md)
- [Core Phase 1–3 acceptance plan](roadmap/CORE_ACCEPTANCE.md)
- [ADR-0001 — Foundational architecture](decisions/ADR-0001-foundation.md)

## Reading rules

1. A **decision** records the current product planning baseline; an **implementation specification** must refine interfaces, storage schema, and protocol details before coding.
2. A **phase** is an ordered product outcome, **not** permission to postpone testing, security, or operational hygiene to a later phase.
3. **Core** does not know manufacturing or building business concepts; domain applications use common core services and add their own semantics.
4. Support for a protocol does not imply control authority or support for every feature/profile of that protocol.
5. **Quervant and AI are not prerequisites** for any core or first-domain functionality.

All scope changes should update the roadmap and, for architectural changes, an ADR.
