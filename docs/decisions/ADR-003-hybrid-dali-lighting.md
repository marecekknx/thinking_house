# ADR-003: Hybrid DALI Lighting

## Status

Accepted

## Context

The house will likely include dimmable living-room lighting, a large recessed LED square, dining-table spots, kitchen lighting and other scene-based lighting. Pure KNX switching would require many actuator channels and would be less flexible for dimming.

## Decision

Use DALI for main and dimmable lighting. Use one KNX switching actuator for simple non-DALI lighting and auxiliary outputs.

## Consequences

- One MDT DALI gateway is planned.
- One MDT 20-channel switching actuator is likely enough.
- DALI drivers must remain service-accessible.
- DALI cable planning must happen before walls and ceilings are closed.
- KNX universal dimmers are not part of the base plan.
