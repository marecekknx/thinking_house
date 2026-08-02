# Project Principles

## Constitution Of The House

1. The house must be usable without internet.
2. The house must be usable without Home Assistant.
3. No critical function may depend on cloud services.
4. Every important system should have a local interface or open protocol.
5. Every automation must have a manual fallback.
6. KNX controls the basic house functions directly.
7. Home Assistant may observe, visualize and optimize, but must not sit in the critical control path.
8. Technology must serve the house. The house must not be redesigned around fragile technology.

## Control-Layer Split

### KNX

KNX owns:

- lights and DALI control
- manual button control
- blinds/shutters
- electric floor heating control
- basic room modes
- presence-driven local functions
- basic alarm-related links
- critical scenes such as Away, Night and All Off

### Home Assistant

Home Assistant owns:

- visualization
- dashboards
- notifications
- PV and battery monitoring
- spot-price optimization
- wallbox optimization
- advanced energy management
- AI decision support
- statistics and long-term history
- non-critical integrations

### Rule

Do not design normal operation like this:

```text
KNX button -> Home Assistant -> KNX actuator
```

Design normal operation like this:

```text
KNX button -> KNX group address -> KNX actuator
                              |
                              +-> Home Assistant observes
```

Home Assistant may send KNX commands, but basic operation must not require it.
