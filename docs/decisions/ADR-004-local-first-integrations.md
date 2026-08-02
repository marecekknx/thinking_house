# ADR-004: Local-First Integrations

## Status

Accepted

## Context

The house will integrate PV, battery storage, wallbox, ventilation, air conditioning, sensors, cameras and future AI workflows. Many consumer devices offer cloud-only integrations, but the house must remain usable without internet.

## Decision

Prefer devices with local APIs, Modbus TCP/RTU, MQTT, KNX, DALI, RTSP/ONVIF or another documented local interface. Cloud services may be used for optimization or convenience, but not as the only control path for important systems.

## Consequences

- Avoid cloud-only devices for infrastructure.
- Prefer Ethernet over Wi-Fi for fixed systems.
- Prefer wired sensors over battery sensors where preparation is possible.
- Home Assistant integrations should be local whenever possible.
- AI may optimize decisions, but local devices or KNX enforce hard limits.
