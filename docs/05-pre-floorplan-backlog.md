# Pre-Floorplan Backlog

These items can be decided or researched before the architectural floor plan is available. The goal is to use waiting time effectively without pretending that room-level design can be finalized early.

## Good To Solve Before Floor Plan

### 1. Finalize Core KNX Distribution Board Direction

Status: mostly decided

- Keep MDT as core KNX manufacturer.
- Keep one KNX TP line unless later floor plan or outdoor scope proves otherwise.
- Keep hybrid lighting: DALI for main/dimmable lighting, KNX switching for simple circuits.
- Confirm whether the listed MDT devices are still the intended first purchase set.

Relevant files:

- `knx/devices.md`
- `knx/physical-addresses.csv`

### 2. Define Technology Selection Criteria

Status: started

Before choosing PV, battery, ventilation, wallbox, AC or cameras, define what each product must support.

Must-have direction:

- local operation
- documented local interface
- Home Assistant compatibility
- no cloud-only dependency for infrastructure
- service availability in Slovakia / Czech Republic
- clear fallback behavior

Relevant files:

- `hardware/selection-principles.md`
- `docs/decisions/ADR-004-local-first-integrations.md`

### 3. Research PV + Battery Ecosystems

Status: decided

Decision:

```text
3x Victron MultiPlus-II 48/5000/70-50
1x Cerbo GX Mk2
minimum 3x Pylontech US5000 at start
target expansion to approximately 5-6x US5000
dedicated critical-load backup board
```

Fallback / benchmark options:

- Deye or similar hybrid inverter + Pylontech as price/performance fallback
- Fronius + BYD as higher-cost premium benchmark
- other locally supported hybrid systems only if they beat the accepted direction on openness, service, backup and price

Remaining questions:

- Should PV be DC-coupled through Victron MPPT chargers, AC-coupled through a PV inverter, or mixed?
- Can PV keep charging the battery during grid outage?
- What is the exact critical-load list and expected 24 h energy budget?
- What are the exact supplier warranty and service terms?

Relevant files:

- `energy/strategy.md`
- `energy/fve-model-shortlist.md`
- `docs/decisions/ADR-005-victron-pylontech-three-phase-ess.md`

### 4. Define Backup Circuit Philosophy

Status: started

Target:

- maintain basic operation for about 24 h during grid outage
- do not include electric floor heating
- fireplace is winter heat backup

Likely backed-up loads:

- KNX
- network rack
- Home Assistant
- heat recovery ventilation
- fridge/freezer
- selected LED lighting
- selected service sockets
- PV/battery control
- basic alarm/security

Open:

- exact critical-load list
- expected standby consumption
- target usable battery capacity
- detailed backup board layout

Relevant file:

- `energy/strategy.md`

### 5. Define Wallbox Requirements

Status: open

Future wallbox should support:

- PV surplus charging
- dynamic load management
- local API / Modbus TCP / OCPP
- Home Assistant integration
- configurable minimum and maximum charging current
- ability to allow short grid-assisted charging
- future spot-price optimization

Do not choose the wallbox before PV/battery ecosystem direction is clearer.

### 6. Define Ventilation Integration Requirements

Status: open

Heat recovery ventilation should:

- keep its own safe controller
- expose local Modbus TCP/RTU, local API or KNX
- provide current mode, fan level, filter status and alarms
- accept Boost / Comfort / Away commands
- remain safe without Home Assistant

Sensors can be prepared now conceptually:

- CO2 in living room, bedroom, office and both children rooms
- humidity in both bathrooms

### 7. Decide Presence Sensor Strategy

Status: partially decided

Presence detection planned for:

- hallway
- bathroom 1
- bathroom 2
- office
- living room
- future garage

Open:

- specific sensor models
- whether office/living room need higher-grade true-presence/radar sensor
- exact mounting locations after floor plan

### 8. Define Alarm Philosophy

Status: started

Direction:

- not an expensive professional alarm as first priority
- but do not rely only on Wi-Fi cameras or Home Assistant
- prepare wired contacts
- use local logic and local siren/alert path where possible

Open:

- whether contacts go to KNX binary inputs, separate alarm controller, or both
- exact number of window contacts
- tilt/open detection per window

### 9. Prepare Documentation Standards

Status: started

Before floor plan, define:

- cable naming scheme
- device naming scheme
- room file naming
- group address naming
- ADR format for decisions
- photo documentation rules during construction

Relevant files:

- `cable-book/cables.csv`
- `docs/rooms/00-room-index.md`
- `docs/04-room-planning-template.md`

## Better To Wait For Floor Plan

Do not finalize these yet:

- exact button positions
- exact sensor positions
- exact DALI branch routing
- exact light circuit count
- exact KNX group addresses per room
- exact number of binary inputs
- exact cable lengths
- exact distribution-board terminal layout
- final AP/camera placement
- exact blind channels beyond known count

## Suggested Waiting-Time Plan

### Week 1

- Estimate critical backup load energy for 24 h.
- Define backup board circuit target.
- Define wallbox requirements.

### Week 2

- Research ventilation units by integration quality.
- Research presence detector options.
- Define alarm/contact strategy.

### Week 3

- Clean up documentation standards.
- Prepare questions for architect/electrician.
- Prepare first floor-plan review checklist.

## First Floor Plan Review Checklist

When the first plan arrives, immediately check:

- technical room size and wall space
- distribution board and rack placement
- cable route feasibility
- window and door count
- blind count and orientation
- living room LED square feasibility
- dining table position
- kitchen island/worktop lighting
- office desk position
- sensor visibility in hallway, bathrooms, office and living room
- future garage/terrace/pool/irrigation conduit paths
