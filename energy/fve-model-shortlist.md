# FVE Model Shortlist

## Context

This shortlist is for a 150 m2 passive-standard bungalow with:

- KNX as the local reliable control layer
- Home Assistant as EMS / visualization / AI layer
- PV, battery and future EV charging
- minimum PV size around 10 kWp
- spot-price optimization
- 24 h backup for critical loads, excluding electric floor heating
- preference for Pylontech if the ecosystem supports it well
- initial battery plan: minimum 3x Pylontech US5000, with future expansion

## Preferred Victron Direction

### Important Correction

PV array size and MultiPlus size are not the same thing.

The MultiPlus-II is primarily the battery inverter/charger and backup power component. A 10 kWp PV array does not automatically require a 15 kVA MultiPlus. It depends on:

- whether PV is DC-coupled through Victron MPPT chargers
- whether PV is AC-coupled through a PV inverter
- whether the PV inverter is connected on the backed-up AC output
- whether PV must keep working during grid outage
- whether the house backup should be single-phase or three-phase
- the real backed-up load, not just PV panel size

### Recommended Victron Architecture For 10 kWp PV

For this house, my preferred Victron architecture is:

```text
3x Victron MultiPlus-II 48/5000/70-50
1x Cerbo GX Mk2
Pylontech US5000 / US5000B battery bank
10 kWp PV via Victron MPPT chargers or a properly designed AC-coupled PV inverter
critical-load or selected-house-load backup board
```

This gives a balanced three-phase Victron system and avoids concentrating the backup system on one phase.

### Why 3x 48/5000 Instead Of 1x 48/15000

For a European three-phase house, 3x MultiPlus-II 48/5000 is usually a more natural architecture than 1x MultiPlus-II 48/15000:

- balanced three-phase operation
- cleaner phase distribution
- better fit with a three-phase house supply
- avoids putting all backed-up loads on one strong phase
- similar total inverter power class, but distributed across phases
- lower per-unit DC current stress
- easier staged thinking around critical loads

### Battery Baseline: 3x Pylontech US5000

The initial battery plan is at least:

```text
3x Pylontech US5000
```

This equals:

- 14.4 kWh nominal capacity
- about 13.68 kWh usable capacity
- 240 A recommended combined charge/discharge current
- 300 A maximum continuous combined charge/discharge current, subject to temperature and BMS limits

This is a much better starting point than a small battery bank. It is enough for a serious critical-load backup design and can support larger inverter options if current limits are configured sensibly.

However, it is still not a battery bank I would abuse with a 15 kVA inverter at full output for long periods. For long-term battery life, the design should respect the recommended current, not just the absolute maximum.

### When 1x MultiPlus-II 48/15000/200-100 Makes Sense

The MultiPlus-II 48/15000/200-100 becomes interesting if:

- the backup board is intentionally single-phase
- many backed-up loads should run from one strong phase
- a large AC-coupled PV inverter must be placed on the backed-up AC output
- the battery bank is sized large enough for the current demand
- the installer confirms grid-code and distribution-board implications
- charge/discharge limits are configured conservatively until the battery bank is expanded beyond 3x US5000

It is not wrong, but it is a heavier and more demanding design.

According to Victron's technical specifications, the 48/15000 class provides 15 kVA / 12 kW continuous power at 25 C, 10 kW at 40 C, 27 kW peak power, 200 A charger current and 55 W zero-load power. That is a serious device and must be matched with a serious battery bank and DC installation.

### Battery Sizing Implication

The 48/15000 option should not be combined with a small Pylontech bank.

For this project, if using 48/15000, 3x US5000 can be a starting point only with sensible current limits. Treat approximately 5x Pylontech US5000-class modules as the more comfortable target for this inverter class, and validate the exact number against:

- Pylontech datasheet current limits
- Victron Pylontech minimum sizing guidance
- expected backup load
- maximum charge current
- maximum discharge current
- desired battery lifetime

With 3x US5000, the 48/15000 should be seen as an oversized-but-expandable inverter choice. That can be acceptable if the roadmap clearly includes more battery modules.

### Smaller Critical-Load Backup Variant

If only selected basic circuits need backup, this lower-cost option remains valid:

```text
1x MultiPlus-II 48/5000/70-50
1x Cerbo GX Mk2
Pylontech battery bank
critical-load backup board
10 kWp PV not necessarily all on backed-up output
```

This variant can still coexist with a 10 kWp PV array. It just means the full PV array may not be available during a grid outage unless the PV topology is designed for it.

### Use With

Use with:

- Cerbo GX Mk2 or current equivalent GX device
- Pylontech US5000 / US5000B battery modules
- Victron VE.Can to CAN-bus BMS type A cable for Pylontech
- Victron MPPT chargers or a properly designed AC-coupled PV inverter architecture
- dedicated backed-up critical-load sub-distribution board

### Why MultiPlus-II 48/5000 Is Still Relevant

The MultiPlus-II 48/5000/70-50 is still the best balanced Victron building block for this project:

- officially documented by Victron as compatible with Pylontech through GX / Venus OS architecture
- strong local integration through GX, MQTT and Modbus TCP
- enough power for critical backed-up loads
- expandable into three-phase operation using three units
- more reasonable battery-current requirements than larger 8 kVA / 10 kVA / 15 kVA units
- strong fit for future Home Assistant / EMS / AI control

### Why Not Default To MultiPlus-II 48/8000

The 48/8000 is technically attractive, but for this project it is not my first choice:

- higher cost
- higher idle consumption
- more demanding DC design
- higher battery current requirements
- unnecessary if the first goal is critical-load backup, not whole-house backup

Use 48/8000 only if the backed-up load calculation proves that 48/5000 is too small but 48/15000 is excessive.

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

For a 10 kWp PV project, choose one of these two Victron directions:

Preferred if budget allows:

```text
3x Victron MultiPlus-II 48/5000/70-50
Cerbo GX Mk2
Pylontech US5000 / US5000B battery bank
```

Possible but more demanding:

```text
1x Victron MultiPlus-II 48/15000/200-100
Cerbo GX Mk2
minimum 3x Pylontech US5000 / US5000B at start
target 5x or more Pylontech US5000 / US5000B over time
single-phase high-power backup design
```

The 48/15000 option should be selected because of backed-up load and topology requirements, not merely because the PV array is 10 kWp.

### If Choosing Deye / Sunsynk

Choose:

```text
Deye SUN-12K-SG05LP3-EU-SM2
Pylontech US5000 / US5000B battery bank
```

Accept the Deye/Sunsynk route only if the supplier proves local integration and official Pylontech compatibility for the exact model.

## Decision Bias

My current project-specific preference:

1. 3x Victron MultiPlus-II 48/5000/70-50 + Pylontech, if budget and installer quality are acceptable
2. Deye SUN-12K-SG05LP3-EU-SM2 + Pylontech, if the price difference is large and local integration is proven
3. 1x Victron MultiPlus-II 48/15000/200-100 + 3x Pylontech US5000 at start, only if a strong single-phase backup design is intentional and battery expansion is planned

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
