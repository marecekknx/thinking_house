# Inverter Ecosystem Comparison

## Working Recommendation

For this house, the current ranking is:

1. Victron + Pylontech
2. Deye/Sunsynk-type hybrid inverter + Pylontech
3. Fronius + BYD

Direct Fronius + Pylontech is currently not recommended as a primary option unless a supplier can prove official compatibility for the exact Fronius inverter and exact Pylontech battery model.

This is not a quality ranking. It is a fit-for-this-project ranking.

The project values:

- local-first operation
- Home Assistant / EMS control
- future AI optimization
- PV surplus EV charging
- spot-price logic
- modular expansion
- 24 h backup for critical loads
- good price/performance
- no cloud-only dependency for core infrastructure

## Option 1: Victron + Pylontech

### Fit

Best architectural fit for this project if budget and installer competence allow it.

### Why It Fits

- Victron officially documents Pylontech compatibility.
- The Pylontech Low Voltage ESS compatibility list Ver. 2.46 also lists Victron MultiPlus 48 V and Quattro 48 V via Venus OS.
- Pylontech US5000 / US5000B are listed in Victron's Pylontech compatibility documentation.
- Victron supports ESS, grid backup and off-grid style designs.
- GX devices expose local MQTT and Modbus TCP.
- Home Assistant has an official Victron GX integration using MQTT.
- The system is modular and highly configurable.
- Good fit for future energy management and AI control.

### Strengths

- strongest local integration story
- very good Home Assistant fit
- good with Pylontech
- excellent for advanced EMS logic
- can be built very robustly
- good observability and diagnostics
- flexible backup architecture

### Weaknesses

- higher design complexity
- more individual components
- needs a very competent installer
- can become expensive if built as a full 3-phase high-power system
- 48 V battery systems require careful DC design and enough battery modules

### Key Design Watch Point

Do not undersize the Pylontech bank. Battery current limits matter. A powerful inverter with too few battery modules is a bad design.

## Option 2: Deye / Sunsynk-Type Hybrid Inverter + Pylontech

### Fit

Potentially very good price/performance, but must be validated at exact model and supplier level.

### Why It Fits

- Deye hybrid inverters advertise support for lithium batteries and multiple communication interfaces including RS485/RS232/CAN.
- The Pylontech Low Voltage ESS compatibility list Ver. 2.46 lists Deye/Sunsynk SUN-SG01LP1, SUN-SG03LP1, SUN-SG04LP1, SUN-SG04LP3, SUN-SG05LP3 and SUN-OG02LP1 series.
- Deye low-voltage hybrid models can fit 48 V battery ecosystems.
- Deye offers built-in hybrid behavior, backup/UPS-style functionality and time-period based charge/discharge configuration.
- Pylontech can be attractive here because it keeps battery cost down.

### Strengths

- usually lower system cost than Victron
- compact all-in-one hybrid inverter
- good feature set on paper
- useful backup/load output features
- often popular with Pylontech-style 48 V batteries
- simpler bill of materials than Victron

### Weaknesses

- integration quality depends heavily on exact model, firmware and data logger
- Home Assistant support is usually less clean than Victron/Fronius
- often relies on Modbus, Solarman/Sunsynk-style integrations, SolarAssistant or community tooling
- local write/control support must be verified before purchase
- supplier and installer quality matter a lot
- official battery compatibility list must be checked for exact inverter model

### Key Design Watch Point

Do not accept a generic claim like "supports Pylontech". Require the exact inverter model, exact battery model, BMS communication method, firmware version and warranty statement.

## Option 3: Fronius + BYD

### Fit

Technically strong and premium, but probably not the best price/performance fit unless the complete supplier offer is excellent.

### Why It Fits

- Fronius officially lists BYD Battery-Box Premium HVS/HVM compatibility with GEN24 Plus families.
- Fronius has good local monitoring through Solar API and Modbus TCP.
- Home Assistant has an official Fronius integration.
- GEN24 Plus offers PV Point and Full Backup options depending on model/configuration.

### Strengths

- clean premium ecosystem
- strong official inverter + battery compatibility
- good market reputation
- good Home Assistant monitoring
- Solar API is local and well documented
- Modbus TCP exists for deeper integration/control
- high-voltage BYD architecture can be elegant and compact

### Weaknesses

- BYD battery cost is significantly higher in many offers
- Home Assistant Solar API integration is read-oriented; control requires Modbus work
- less open/flexible than Victron for custom EMS
- backup functionality has specific Fronius constraints and hardware requirements
- may be overpaying if the premium ecosystem does not solve a real project need

### Key Design Watch Point

Fronius + BYD should be kept as premium benchmark. Choose it only if the total installed offer, warranty, service and backup behavior justify the price premium.

## Rejected / High-Risk Option: Fronius + Pylontech Direct Hybrid

### Fit

Not recommended as a direct hybrid battery pairing at this stage.

### Why

The official Fronius compatible battery information for GEN24 / GEN24 Plus points to Fronius Reserva / Reserva Pro, BYD Battery-Box and LG Flex families, depending on inverter model and country certification. Pylontech is not listed in the current Fronius compatible battery overview checked for this project.

The user-provided Pylontech Low Voltage ESS compatibility list Ver. 2.46, last updated 2026-07-07, also lists many inverter brands including Victron and Deye/Sunsynk, but Fronius was not found in the extracted list.

That means a direct design like this should be treated as unsupported unless proven otherwise:

```text
Fronius GEN24 Plus
    |
    +-- Pylontech battery on the inverter battery port
```

### Why It Is Tempting

- Fronius has a good reputation and good Home Assistant monitoring.
- Pylontech has attractive price per kWh.
- Combining both sounds like a way to get Fronius quality with cheaper storage.

### Why It Is Risky

- battery communication may not work reliably
- firmware updates can break unofficial combinations
- installer support may be weak
- warranty responsibility becomes unclear
- backup behavior may not be certified
- BMS limits may not be correctly respected

### Accept Only If

A supplier provides written confirmation for:

- exact Fronius inverter model
- exact Pylontech battery model
- official compatibility source
- supported BMS communication method
- warranty coverage for the pairing
- backup behavior during grid outage
- local integration path for Home Assistant / EMS

Without that, this option should be rejected.

## Alternative: Fronius PV + Victron/Pylontech AC-Coupled Storage

There is a different architecture where Fronius is used as a PV inverter and Victron + Pylontech handles storage and backup:

```text
PV panels
    |
Fronius PV inverter
    |
AC bus
    |
Victron inverter/charger + GX
    |
Pylontech battery
```

This is not the same as "Fronius hybrid + Pylontech". It is an AC-coupled architecture.

It can be technically strong because Victron documents AC-coupled PV with Fronius PV inverters and also documents Pylontech battery compatibility. However, it is more complex and should only be designed by an installer who understands Victron ESS / backup systems well.

For this house, it could make sense only if:

- there is a strong reason to use Fronius PV inverters
- Victron is still used as the storage / backup / EMS layer
- the additional complexity and cost are justified

Otherwise, a cleaner Victron + Pylontech design is probably better.

## Comparative Summary

| Criterion | Victron + Pylontech | Deye/Sunsynk-Type + Pylontech | Fronius + BYD | Fronius + Pylontech Direct |
|---|---|---|---|---|
| Openness | Excellent | Medium to good, model-dependent | Good for monitoring, less open for control | Poor / unsupported unless proven |
| Home Assistant fit | Excellent | Medium, often community/SolarAssistant | Good for monitoring | Unclear |
| Local control | Excellent | Must verify | Possible via Modbus, more constrained | Unclear |
| Price/performance | Medium | Potentially excellent | Usually weaker | Tempting on paper, risky in practice |
| Installation simplicity | Medium/complex | Good | Good | Risky if unofficial |
| Advanced EMS / AI | Excellent | Good if Modbus/control works | Medium | Unclear |
| Battery cost | Good with Pylontech | Good with Pylontech | Higher with BYD | Good battery cost, but compatibility risk |
| Official compatibility clarity | Strong | Must verify per model | Strong | Not found in Fronius list |
| Backup flexibility | Excellent | Good, model-dependent | Good but constrained | Unclear / not recommended |
| Long-term tinkering | Excellent | Medium/good | Medium | Poor if unsupported |

## Current Shortlist

### Primary Direction

Victron + Pylontech.

Use this as the architectural target unless the price becomes unreasonable.

### Budget / Price-Performance Challenger

Deye/Sunsynk-type hybrid inverter + Pylontech.

Keep only if exact model has:

- official Pylontech compatibility
- local Modbus or other local control path
- good Slovak/Czech installer support
- clear backup behavior
- documented warranty compatibility

### Premium Benchmark

Fronius + BYD.

Use for comparison against a well-supported premium offer. Do not choose it just because it is premium.

### Do Not Shortlist Without Proof

Fronius + Pylontech as a direct hybrid pairing.

Keep it out of the shortlist unless a supplier provides written proof of official compatibility for the exact models.

## Questions For Installers

Ask every supplier:

1. What exact inverter model are you proposing?
2. What exact battery model is officially compatible?
3. Is the compatibility stated by the inverter manufacturer, battery manufacturer, or only your experience?
4. Does the inverter expose local Modbus TCP/RTU, MQTT or API?
5. Can Home Assistant read battery SoC, PV power, grid import/export and house load locally?
6. Can Home Assistant or EMS locally limit charging/discharging or set schedules?
7. What happens during internet outage?
8. What happens during Home Assistant outage?
9. What circuits can be backed up?
10. Is backup single-phase or three-phase?
11. What is the transfer time to backup?
12. Can PV charge the battery during grid outage?
13. Can the battery be charged from grid according to spot price?
14. What warranty applies to the exact inverter + battery pairing?
15. What is the guaranteed battery throughput or remaining capacity?
16. Who provides local service and replacement?

## Current Decision

Do not select the final FVE ecosystem yet.

Next step:

- collect rough installed prices for all three archetypes
- estimate critical backup load energy for 24 h
- decide whether backup should be single-phase critical-load backup or more ambitious three-phase backup

## Sources

- User-provided PDF: Compatibility List of Pylontech Low Voltage ESS and Inverters Ver. 2.46, last update 2026-07-07
- Victron + Pylontech compatibility: https://www.victronenergy.com/live/battery_compatibility:pylontech_phantom
- Victron GX Modbus TCP manual: https://www.victronenergy.com/live/ccgx:modbustcp_faq
- Home Assistant Victron GX integration: https://www.home-assistant.io/integrations/victron_gx/
- Home Assistant Modbus integration: https://www.home-assistant.io/integrations/modbus
- Fronius battery compatibility overview: https://www.fronius.com/en-gb/uk/solar-energy/installers-partners/technical-data/all-products/storage-units/battery-overview/battery-overview
- Fronius GEN24 product guide: https://www.fronius.com/en-gb/uk/solar-energy/installers-partners/service-support/tech-support/how-to-install/installation-guide-gen24
- Fronius Solar API: https://www.fronius.com/en-us/usa/solar-energy/installers-partners/technical-data/all-products/system-monitoring/open-interfaces/fronius-solar-api-json-
- Home Assistant Fronius integration: https://www.home-assistant.io/integrations/fronius/
- Deye hybrid inverter category: https://deye.com/product-category/inverter/hybrid-inverter/
- Current Fronius compatible batteries overview: https://www.fronius.com/en/solar-energy/solar-solutions/solar-energy-storage/compatible-batteries
- Victron AC-coupled PV with Fronius PV inverters: https://www.victronenergy.com/live/ac_coupling:fronius
