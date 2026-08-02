# ADR-002: Home Assistant Is A Non-Critical Layer

## Status

Accepted

## Context

Home Assistant is powerful for integrations, visualization, energy management and AI workflows, but it is still a server that can restart, update or fail.

## Decision

Home Assistant is used for comfort, visualization, advanced automation, energy management, spot-price logic and AI optimization. It is not required for basic operation of lights, blinds or heating.

## Consequences

- HA dashboards and automations can be improved freely without risking basic house operation.
- Critical safety limits must live in KNX, in dedicated devices, or inside the relevant manufacturer system.
- HA may optimize, but local devices must enforce hard limits.
