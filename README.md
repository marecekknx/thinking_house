# Smart House Design

Living design repository for a 150 m2 bungalow with KNX as the local control backbone, DALI lighting, Home Assistant as a non-critical integration and energy layer, PV, battery storage, future garage, terrace, wallbox, pool and irrigation.

## Core Principle

Critical functions are local and reliable. Comfort functions may live in Home Assistant.

In practice:

- KNX is the house backbone.
- Home Assistant is the visualization, integration, energy and AI layer.
- The house must remain normally usable without internet.
- The house must remain normally usable without Home Assistant.
- Cloud services may optimize, but must not be required for basic operation.

## Current Status

- House type: bungalow
- Approximate usable area: 150 m2
- Technical room: yes
- Main automation: KNX / MDT
- Lighting strategy: hybrid DALI + KNX switching
- Heating: electric floor heating
- Cooling: backup air conditioning, likely 1 outdoor unit and max. 2 indoor units
- Ventilation: heat recovery ventilation, integration to be selected
- Energy: Victron three-phase ESS + Pylontech battery bank + future AI energy management
- Accepted ESS direction: 3x Victron MultiPlus-II 48/5000/70-50 + Cerbo GX Mk2 + min. 3x Pylontech US5000
- Backup target: 24 h basic house operation without electric heating
- Future stages: garage, covered terrace, EV charging, borehole, garden irrigation, pool

## Repository Layout

- `docs/` - principles, requirements, architecture and decisions
- `knx/` - devices, addresses, I/O lists, DALI planning and ETS notes
- `home-assistant/` - future automations, scripts and dashboards
- `energy/` - PV, battery, wallbox and EMS logic
- `network/` - LAN, Wi-Fi, VLANs and device inventory
- `drawings/` - floor plans and exported PDFs
- `cable-book/` - cable schedule and installation tracking
- `hardware/` - product shortlists and compatibility notes

## Next Trigger

Continue detailed room-by-room planning when a first floor plan or sketch is available.
