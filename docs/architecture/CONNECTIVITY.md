# Core connectivity — capability and safety contract

**Status:** Initial requirements only; concrete Python APIs, schemas, libraries and conformance fixtures follow in Phase 1 design PRs.

## Four required Core adapters

| Adapter | Initial read-side support | Explicit initial exclusions |
|---|---|---|
| **Modbus TCP** | Connection setup, configured register/coil reads, polling, decoding, validity/errors | RTU serial support, arbitrary writes, PLC control |
| **OPC UA** | Endpoint discovery, session/browse, read/subscribe, statuses, server/source timestamps where supplied | Server-side control methods, broad information model authoring, unrestricted writes |
| **MQTT** | Broker connection, topic subscriptions, payload decoding/mapping, QoS/retained-message handling, reconnect | Command publishing, arbitrary broker management |
| **BACnet/IP** | Device/object discovery as topology permits, object/property reads, polling, COV subscriptions where supported, status/quality metadata | MS/TP, BACnet/SC, writes, trend-log completeness claims, routing/network management |

Support the capability when it is advertised and tested. Do not claim a uniform protocol feature set. Ignition interoperability is tested but Ignition is an **optional external system**, not an Indral runtime dependency.

## Shared adapter requirements

1. **Identity:** stable Indral source/endpoint identity; native addresses (Modbus unit/register, OPC UA NodeId, MQTT topic/broker, BACnet device/object/property); explicit mapping to canonical assets/signals.
2. **Capabilities:** advertise discovery, polling, subscription, value shape, metadata and quality availability; reject unsupported operations explicitly.
3. **Lifecycle:** create/configure, validate, connect, enumerate/subscribe where applicable, ingest, pause/retry, stop/cleanup; expose clear states and health.
4. **Observations:** carry normalized value/type/unit when known, raw/native locator, quality/status, source timestamp when supported, first reception time and Indral persisted time. Unknown units and timestamps stay unknown.
5. **Delivery:** account for duplicates, out-of-order arrivals, buffering, lost intervals, reconnect and replay; never silently infer complete data coverage.
6. **Errors/telemetry:** structured failures, retry/backoff limits, metrics, trace/correlation IDs; distinguish protocol exception from a process alarm.
7. **Safety:** read-only by default and no generic actuation/write API. Device credentials and network configuration must not be logged.

## Important non-equivalences

- **Modbus** exposes configured addresses; the adapter may not know engineering units or asset semantics without mapping.
- **OPC UA** exposes typed nodes and relationships; preserve information-model references and server metadata where available.
- **MQTT** exposes topics and payloads; ordering/QoS guarantees depend on broker, session, topic, and consumer behavior. No universal source timestamp exists.
- **BACnet** has device/object/property identity, network discovery constraints and change-of-value notifications. IP broadcasts may not cross subnets/containers; provide explicit known-device configuration as a test path.

## Phase 1 protocol validation matrix

- Adapter can ingest a known deterministic synthetic measurement.
- Native identity and normalized identity are both retained.
- Read failures, disconnections, restart and malformed values are surfaced with diagnostic states.
- A second source with the same display label does not collide with the first.
- Lack of source timestamps is handled explicitly.
- Capability tests verify rejected writes/controls.
- BACnet discovery and known-device configurations are both covered in suitable local test topologies.
- OPC UA subscriptions and BACnet COV are tested where fixtures support them; unsupported capability is reported, not fabricated.

## Phase 2 integration

Each adapter must feed the *same* historian/event intake contract, with source-specific metadata preserved. UI and core historical queries must not branch on assumptions like "every measurement came from a PLC" or "all BACnet values are HVAC values".

Final selection of Python libraries, transport/version support and precise coverage must be locked in before implementing each adapter.
