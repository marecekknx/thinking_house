# FVE Model Shortlist

## Context

This shortlist is for a 150 m2 passive-standard bungalow with:

- KNX as the local reliable control layer
- Home Assistant as EMS / visualization / AI layer
- PV, battery and future EV charging
- minimum PV size around 10 kWp
- spot-price optimization
- 24 h backup for critical loads, excluding electric floor heating
- initial battery plan: minimum 3x Pylontech US5000, with future expansion

## Accepted Victron Direction

The accepted project direction is:

```text
3x Victron MultiPlus-II 48/5000/70-50
1x Cerbo GX Mk2
minimum 3x Pylontech US5000 at start
target expansion to approximately 5-6x Pylontech US5000 over time
minimum 10 kWp PV
dedicated backed-up sub-distribution board for critical loads
```

This is now an accepted architecture decision, not only a shortlist preference. See `docs/decisions/ADR-005-victron-pylontech-three-phase-ess.md`.

## Important Correction

PV array size and MultiPlus size are not the same thing.

The MultiPlus-II is primarily the battery inverter/charger and backup power component. A 10 kWp PV array does not automatically require a 15 kVA MultiPlus. It depends on:

- whether PV is DC-coupled through Victron MPPT chargers
- whether PV is AC-coupled through a PV inverter
- whether the PV inverter is connected on the backed-up AC output
- whether PV must keep working during grid outage
- whether the house backup should be single-phase or three-phase
- the real backed-up load, not just PV panel size

## Why 3x 48/5000 Instead Of 1x 48/15000

For a European three-phase house, 3x MultiPlus-II 48/5000 is a more natural architecture than 1x MultiPlus-II 48/15000:

- balanced three-phase operation
- cleaner phase distribution
- better fit with a three-phase house supply
- avoids putting all backed-up loads on one strong phase
- similar total inverter price class based on current observed prices
- lower per-unit DC current stress
- easier staged thinking around critical loads

The 1x MultiPlus-II 48/15000/200-100 remains technically valid, but should be selected only if the project intentionally wants a strong single-phase backup design.

## Battery Baseline: 3x Pylontech US5000

The initial battery plan is at least:

```text
3x Pylontech US5000
```

This equals approximately:

- 14.4 kWh nominal capacity
- about 13.68 kWh usable capacity
- 240 A recommended combined charge/discharge current
- 300 A maximum continuous combined charge/discharge current, subject to temperature and BMS limits

This is enough for a serious critical-load backup design, but the design should still respect recommended current limits. The target expansion is approximately 5-6x US5000 modules over time.

## Backup Board Direction

Use a dedicated critical-load sub-distribution board.

Back up by default:

- KNX power supply and IP communication
- router, switch and internet equipment
- Home Assistant
- heat recovery ventilation
- fridge/freezer
- selected LED lighting
- selected service sockets
- security / camera basics
- future garage door if appropriate

Do not back up by default:

- electric floor heating
- hob
- oven
- EV wallbox
- boiler / DHW heating
- washing machine / dryer
- pool equipment
- garden irrigation

The PV system may still support the whole house during normal grid-connected operation. The backup board only defines what remains powered during grid outage.

## Remaining PV Topology Decision

The accepted ESS direction does not yet decide how PV panels connect.

Still open:

- Victron MPPT chargers / DC-coupled PV
- AC-coupled PV inverter
- mixed design
- whether PV should continue charging the battery during grid outage
- exact roof orientation and string design

This should be decided later with the roof plan and installer.

## Fallback: Deye / Sunsynk + Pylontech

Deye SUN-12K-SG05LP3-EU-SM2 remains the price/performance fallback.

Accept Deye/Sunsynk only if the supplier proves:

- exact model compatibility with Pylontech
- CAN/RS485 BMS communication details
- Modbus TCP or RTU access
- whether write/control registers are supported locally
- whether logger/cloud can be bypassed for local Home Assistant integration
- backup output behavior
- warranty coverage for the exact inverter + battery combination

## Premium Benchmark: Fronius + BYD

Fronius + BYD remains a premium benchmark, but is not the selected direction because BYD batteries appear significantly more expensive and the added value does not currently justify the price difference for this project.

## Rejected: Direct Fronius + Pylontech

Direct Fronius hybrid + Pylontech is not selected. Current compatibility evidence does not support direct Fronius hybrid operation with Pylontech low-voltage batteries.

## Project-Specific Ranking

1. 3x Victron MultiPlus-II 48/5000/70-50 + Pylontech
2. Deye SUN-12K-SG05LP3-EU-SM2 + Pylontech, if the price difference is large and local integration is proven
3. 1x Victron MultiPlus-II 48/15000/200-100 + Pylontech, only if a strong single-phase backup design is intentional
4. Fronius + BYD only if a premium supplier offer clearly justifies the price premium

This is a reliability / openness / maintainability decision, not a brand-prestige decision.

## Sources

- Victron MultiPlus-II product page: https://www.victronenergy.com/inverters-chargers/multiplus-ii
- Victron MultiPlus-II 230 V technical specifications: https://www.victronenergy.nl/media/pg/MultiPlus-II_230V/en/technical-specifications-mp-ii-230v.html
- Victron + Pylontech compatibility: https://www.victronenergy.com/live/battery_compatibility:pylontech_phantom
- Home Assistant Victron GX integration: https://www.home-assistant.io/integrations/victron_gx/
- Deye product datasheet page: https://www.deyeinverter.com/download/product-2/
- User-provided PDF: Compatibility List of Pylontech Low Voltage ESS and Inverters Ver. 2.46, last update 2026-07-07
