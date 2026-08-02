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

Pylontech is the accepted battery direction because of price/performance, modularity and compatibility with the selected Victron ESS architecture.

Accepted ESS direction:

```text
3x Victron MultiPlus-II 48/5000/70-50
1x Cerbo GX Mk2
minimum 3x Pylontech US5000 at start
target expansion to approximately 5-6x US5000
dedicated critical-load backup board
```

The battery must still be validated in the final supplier design against exact Pylontech model, Victron compatibility guidance, current limits, protection design, warranty terms and local service availability.

## Fallback Ecosystems

Deye / Sunsynk + Pylontech remains the price/performance fallback if the Victron system becomes financially unreasonable.

Fronius + BYD remains a premium benchmark, but is not the selected direction because the current price difference for BYD batteries does not appear justified for this project.
