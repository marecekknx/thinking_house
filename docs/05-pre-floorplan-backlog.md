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

Status: open

Compare ecosystems, not only batteries.

Candidates:

- Victron + Pylontech
- Deye or similar hybrid inverter + Pylontech
- Fronius + BYD as higher-cost benchmark
- other locally supported hybrid systems with good Modbus/Home Assistant support

Questions to answer:

- Does it support local Modbus TCP/RTU or MQTT?
- Can Home Assistant read PV, grid, battery and inverter state locally?
- Can charging/discharging be controlled or limited locally?
- Is backup output suitable for selected critical loads?
- What is the official battery compatibility list?
- What are warranty limits in cycles/MWh and remaining capacity?
- How good is local service?

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
- backup inverter output requirements

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

- Research PV/battery ecosystems.
- Define backup circuit target and rough energy budget.
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
