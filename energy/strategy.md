# Energy Strategy

## Goals

- Minimize dependence on the energy supplier.
- Use PV production locally when sensible.
- Use spot prices for buying and selling energy.
- Charge the future EV primarily from PV surplus.
- Allow short grid-assisted EV charging when useful.
- Keep basic systems alive for approximately 24 h during grid outage.

## Backup Scope

Backup should include:

- KNX power supply and IP communication
- Home Assistant
- router, switch and internet equipment
- heat recovery ventilation
- fridge/freezer
- selected LED lighting
- selected service sockets
- PV/battery control equipment
- future security/alarm basics
- future garage door if appropriate

Backup should not include by default:

- electric floor heating
- hob
- oven
- boiler / DHW heating
- EV wallbox
- pool equipment
- garden irrigation

## Battery Direction

Pylontech remains a preferred candidate because of price/performance and modularity. Final selection depends on inverter compatibility, local integration, warranty terms and Slovak/Czech service availability.

Candidate ecosystems to evaluate later:

- Victron + Pylontech
- compatible hybrid inverter + Pylontech
- Fronius + BYD as a higher-cost benchmark

Do not select the battery before selecting the full inverter + battery + backup + EMS ecosystem.
