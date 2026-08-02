# ADR-005: Victron And Pylontech Three-Phase ESS

## Status

Accepted

## Context

The house is planned as a 150 m2 passive-standard bungalow with KNX as the local reliable control layer, Home Assistant as the EMS / visualization / AI layer, at least 10 kWp of PV, battery storage, future EV charging and spot-price optimization.

The backup goal is not whole-house backup. The goal is to keep basic systems alive for approximately 24 h during a grid outage, excluding electric floor heating and other high-load appliances.

The initial battery plan is at least 3x Pylontech US5000, with future expansion expected.

## Decision

Use a Victron three-phase ESS architecture with Pylontech low-voltage batteries as the primary project direction:

```text
3x Victron MultiPlus-II 48/5000/70-50
1x Cerbo GX Mk2
minimum 3x Pylontech US5000 at start
target battery expansion to approximately 5-6x US5000 over time
minimum 10 kWp PV
dedicated backed-up sub-distribution board for critical loads
```

The backed-up sub-distribution board should include only critical circuits:

- KNX power supply and KNX IP communication
- router, switch and internet equipment
- Home Assistant
- heat recovery ventilation
- fridge and freezer
- selected LED lighting
- selected service sockets
- security / camera basics
- future garage door if appropriate

The backed-up board should not include by default:

- electric floor heating
- hob
- oven
- EV wallbox
- boiler / DHW heating
- washing machine / dryer
- pool equipment
- garden irrigation

The PV system may still support the whole house during normal grid-connected operation. The dedicated backup board only defines what remains powered during grid outage.

## Rejected Alternatives

### 1x Victron MultiPlus-II 48/15000/200-100

This remains technically valid, but is not the preferred architecture for this house because it creates a strong single-phase backup design. It would make sense only if the project intentionally wanted high-power single-phase backup.

Given the current observed pricing, 3x MultiPlus-II 48/5000 costs almost the same as 1x MultiPlus-II 48/15000 while providing a cleaner three-phase architecture.

### Deye / Sunsynk + Pylontech

This remains the price/performance fallback option. It may be selected later only if the Victron system becomes financially unreasonable and the supplier proves:

- exact model compatibility with Pylontech
- local Modbus / API integration
- backup behavior
- warranty terms
- local service quality

### Fronius + BYD

This remains the premium benchmark, but is not selected because BYD batteries appear significantly more expensive and the added value does not currently justify the price difference for this project.

### Direct Fronius + Pylontech

Not selected. Current compatibility evidence does not support direct Fronius hybrid operation with Pylontech low-voltage batteries.

## Consequences

- The electrical design should include a dedicated critical-load backup board.
- Critical loads may be distributed across three backed-up phases.
- The system stays compatible with the project principle: critical functions local and reliable, comfort functions in Home Assistant.
- Home Assistant can optimize energy flows, spot-price charging and future EV charging, but Victron / Cerbo / battery BMS enforce local operational limits.
- Battery expansion space, DC protection, cabling and ventilation must be planned from the beginning.
- PV topology still needs a later detailed decision: Victron MPPT chargers, AC-coupled PV inverter, or a mixed design.
