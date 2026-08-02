# ADR-001: KNX Is The Core Control System

## Status

Accepted

## Context

The house must remain usable when Home Assistant, internet access, cloud services or experimental AI features are unavailable.

## Decision

KNX is the primary local control layer for the house. Basic lights, blinds, heating, buttons, DALI control and core scenes must work directly in KNX.

## Consequences

- Home Assistant must not be inserted into the critical path for normal button-to-actuator operation.
- ETS group addresses must be designed cleanly and documented.
- Home Assistant may observe KNX states and send non-critical commands.
- KNX logic handles basic local fallback behavior.
