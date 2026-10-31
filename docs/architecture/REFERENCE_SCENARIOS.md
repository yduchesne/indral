# Reference scenarios and validation fixtures

**Goal:** validate Core as a working domain-independent product before adding Manufacturing or Smart Buildings.

## A. Core-only deterministic fixture (Phases 1–3)

The test fixture is not an MES, BAS or actual PLC. It exposes generic assets **A-101**, **A-102**, source points and a dependency edge across independently configured protocol sources.

- A Modbus TCP endpoint exposes numeric process values and a discrete status.
- An OPC UA endpoint exposes typed measurements, state and node identity.
- An MQTT broker carries an event/measurement stream with an explicit application payload contract.
- A synthetic BACnet/IP device exposes analog/binary object properties; exercise polling and supported COV.
- At least one adapter/source must intentionally omit a source timestamp.
- Inject disconnects, duplicates, late data and a native-ID mapping correction.
- At a controlled valid time, reassign the dependency edge A-101 -> A-102 to a new target, preserving both assertions and recording knowledge time.

**Core acceptance walkthrough:**
1. Discover/configure all four sources (including BACnet known-device fallback) and visualize normalized measurements with their source quality.
2. Restart an adapter; show health/recovery and observe that no silent duplicate or fake completeness is reported.
3. Inspect event and alarm history without application-specific business concepts.
4. Select operational time T and knowledge cutoff K; verify historical topology and evidence visibility.
5. Use an incident timeline and graph to correlate measurements and transitions; the UI distinguishes evidence from conclusions.

The fixture must be usable in automated tests with deterministic clock/seed control. Its source systems are not automatically part of the runtime dependency graph.

## B. Manufacturing reference scenario (Phase 4)

**Simulated bottling/packaging line:** tank, transfer pump, conveyor, filling, inspection and packaging stations. Operations include a production order, material lot, produced/rejected counts, an equipment fault, operator intervention and CMMS work order.

**Learning/investigation outcomes:**
- Map line/station/equipment and production context into Core asset identities.
- Track production-order lifecycle, equipment usage and material genealogy.
- Compute OEE from explicit planned production time, actual run time, ideal cycle time, total count and good count; handle zero denominators and missing evidence.
- Explain production delay using telemetry, alarms, maintenance and MES events; identify *possible* causal paths without asserting causation from correlation.
- Query the same incident at multiple knowledge cutoffs after late-arriving evidence.

Simulated MES and CMMS endpoints are separate integrations, not Core tables masquerading as external services.

## C. Smart Buildings reference scenario (Phase 5; optional)

A future independent BAS domain can model an AHU, VAVs, spaces and zones, occupancy schedule and energy data. It should use Core historian, events and temporal graph as-is. The presence of BACnet support in Phase 1 **does not** require a building simulator or any HVAC entity in Core.

**Architectural validation:** adding this domain must not require schema changes to generic source, asset, historian, bitemporal graph or evidence meaning. New domain-owned entities/mappings are permitted.

## D. Evidence-based completion rule

A scenario passes only if automated assertions and a reproducible UI/API demonstration agree. Every failure mode must have a recorded expected outcome; no success criterion depends on a language model or Quervant.
