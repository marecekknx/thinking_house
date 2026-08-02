# Planning Workflow

This project is planned in layers. Each layer should be understandable on its own, and later layers should not break the basic rule: critical functions local and reliable, comfort functions in Home Assistant.

## Layer 1: Floor Plan

Inputs needed:

- PDF floor plan
- room names
- dimensions
- windows and doors
- opening directions
- north orientation
- rough furniture layout
- technical room position

Output:

- room list
- control points
- sensor positions
- cable preparation notes

## Layer 2: Electrical Preparation

Output:

- lighting circuit list
- DALI branches
- non-DALI circuits
- blind motor cables
- floor heating zones
- door/window contacts
- technical-room cable routes
- garage/terrace/pool/irrigation preparation

## Layer 3: KNX

Output:

- KNX device list
- physical addresses
- group address structure
- button functions
- presence detector logic
- heating control logic
- blind logic
- local scenes

## Layer 4: DALI

Output:

- DALI gateway configuration concept
- DALI driver list
- DALI groups
- DALI scenes
- LED strip driver placement
- service access notes

## Layer 5: Network

Output:

- rack layout
- Ethernet outlet list
- access point locations
- camera positions
- VLAN plan
- PoE requirements

## Layer 6: Energy

Output:

- PV inverter selection criteria
- battery strategy
- backup circuit list
- wallbox requirements
- spot-price logic
- Home Assistant EMS concept

## Layer 7: Home Assistant

Output:

- integrations
- dashboards
- helpers
- non-critical automations
- notifications
- energy optimization logic

## Layer 8: AI

Output:

- AI decision boundaries
- cloud-first optimization
- future local AI migration plan
- hard limits that AI may not override
