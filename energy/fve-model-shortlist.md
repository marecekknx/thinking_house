# FVE Model Shortlist

## Context

This shortlist is for a 150 m2 passive-standard bungalow with:

- KNX as the local reliable control layer
- Home Assistant as EMS / visualization / AI layer
- PV, battery and future EV charging
- spot-price optimization
- 24 h backup for critical loads, excluding electric floor heating
- preference for Pylontech if the ecosystem supports it well

## Preferred Victron Direction

### Recommended Core Model

Victron MultiPlus-II 48/5000/70-50

Use with:

- Cerbo GX Mk2 or current equivalent GX device
- Pylontech US5000 / US5000B battery modules
- Victron VE.Can to CAN-bus BMS type A cable for Pylontech
- Victron MPPT chargers or a properly designed AC-coupled PV inverter architecture
- dedicated backed-up critical-load sub-distribution board

### Why This Model

The MultiPlus-II 48/5000/70-50 is the best balanced Victron unit for this project:

- officially documented by Victron as compatible with Pylontech through GX / Venus OS architecture
- strong local integration through GX, MQTT and Modbus TCP
- enough power for critical backed-up loads
- expandable into three-phase operation using three units
- more reasonable battery-current requirements than larger 8 kVA / 10 kVA / 15 kVA units
- strong fit for future Home Assistant / EMS / AI control

### Preferred Starting Architecture

Start with one of these two approaches:

#### Conservative / Critical-Load Backup

```text
1x MultiPlus-II 48/5000/70-50
1x Cerbo GX Mk2
Pylontech battery bank
critical-load backup board
```

This is the most cost-rational starting point if only selected circuits need backup.

#### Full Three-Phase Victron ESS

```text
3x MultiPlus-II 48/5000/70-50
1x Cerbo GX Mk2
larger Pylontech battery bank
three-phase ESS / backup design
```

This is more powerful and elegant, but significantly more expensive and requires more battery capacity.

### Why Not Start With MultiPlus-II 48/8000

The 48/8000 is technically attractive, but for this project it is not my first choice:

- higher cost
- higher idle consumption
- more demanding DC design
- higher battery current requirements
- unnecessary if the first goal is critical-load backup, not whole-house backup

Use 48/8000 only if the backed-up load calculation proves that 48/5000 is too small.

## Preferred Deye / Sunsynk Direction

### Recommended Deye Model

Deye SUN-12K-SG05LP3-EU-SM2

Fallback / older proven family:

Deye SUN-12K-SG04LP3-EU

Sunsynk-branded equivalent:

Sunsynk 12 kW 3-phase low-voltage hybrid inverter, only if the local supplier support and compatibility proof are stronger than for Deye-branded hardware.

### Why This Model

The Deye SUN-12K-SG05LP3-EU-SM2 is the preferred Deye direction because:

- it is three-phase
- it is a low-voltage 48 V hybrid inverter
- it supports lead-acid or lithium-ion batteries with BMS self-adaptation
- the datasheet lists RS485 / CAN communication
- the datasheet lists 6 time periods for battery charge/discharge
- the datasheet lists AC coupling support
- the datasheet lists up to 10 units in parallel
- the datasheet lists 100% unbalanced output, with per-phase output limited by the model rating
- Pylontech's Ver. 2.46 low-voltage compatibility list includes Deye/Sunsynk SUN-SG05LP3 and SUN-SG04LP3 series

### Why 12 kW

For this house I would not choose a 5 kW or 6 kW three-phase unit as the main hybrid inverter.

Reasons:

- future EV charging
- future garage
- future pool / garden loads
- PV surplus management
- spot-price battery charging
- three-phase house supply
- reserve for asymmetric phase loads

The 10 kW model could work. The 12 kW model gives a better reserve if the price difference is reasonable.

### Key Risk

Deye/Sunsynk must be validated at exact model, firmware and integration level.

Before purchase, require written answers for:

- exact model number
- exact Pylontech battery model
- official compatibility reference
- CAN/RS485 BMS communication details
- Modbus TCP or RTU access
- whether write/control registers are supported locally
- whether the logger/cloud can be bypassed for local Home Assistant integration
- backup output behavior
- warranty coverage for the exact inverter + battery combination

## Current Recommendation

### If Choosing Victron

Choose:

```text
Victron MultiPlus-II 48/5000/70-50
Cerbo GX Mk2
Pylontech US5000 / US5000B battery bank
```

Design the system so it can be expanded later to three-phase if needed.

### If Choosing Deye / Sunsynk

Choose:

```text
Deye SUN-12K-SG05LP3-EU-SM2
Pylontech US5000 / US5000B battery bank
```

Accept the Deye/Sunsynk route only if the supplier proves local integration and official Pylontech compatibility for the exact model.

## Decision Bias

My current project-specific preference:

1. Victron MultiPlus-II 48/5000/70-50 + Pylontech, if budget and installer quality are acceptable
2. Deye SUN-12K-SG05LP3-EU-SM2 + Pylontech, if the price difference is large and local integration is proven

This is a reliability / openness / maintainability decision, not a brand-prestige decision.

## Sources

- Victron MultiPlus-II product page: https://www.victronenergy.com/inverters-chargers/multiplus-ii
- Victron MultiPlus-II 230 V technical specifications: https://www.victronenergy.nl/media/pg/MultiPlus-II_230V/en/technical-specifications-mp-ii-230v.html
- Victron + Pylontech compatibility: https://www.victronenergy.com/live/battery_compatibility:pylontech_phantom
- Home Assistant Victron GX integration: https://www.home-assistant.io/integrations/victron_gx/
- Deye product datasheet page: https://www.deyeinverter.com/download/product-2/
- Deye SUN-3/4/5/6/8/10/12K-SG05LP3-EU-SM2 datasheet
- Deye SUN-5/6/8/10/12K-SG04LP3-EU-AM2-P datasheet
- User-provided PDF: Compatibility List of Pylontech Low Voltage ESS and Inverters Ver. 2.46, last update 2026-07-07
