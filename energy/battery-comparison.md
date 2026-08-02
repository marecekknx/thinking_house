# Battery Comparison: Pylontech vs BYD

## Current Working Conclusion

Pylontech is the accepted battery direction for this project with the selected Victron three-phase ESS architecture. BYD should not be chosen only because it is more expensive or assumed to last longer.

The decision was made at ecosystem level:

```text
inverter + battery + backup output + local API + service + warranty
```

not at battery-module level alone.

## Pylontech Strengths

- strong price/performance
- modular 48 V rack-style architecture
- easy capacity expansion
- good fit for open systems such as Victron
- CAN/RS485 communication on US-series modules
- widely used LiFePO4 technology
- good match for a technically managed Home Assistant / EMS project

## Pylontech Risks / Watch Points

- 48 V systems mean higher current for the same power
- cabling, fusing, busbars and installation quality matter a lot
- enough modules must be installed to support inverter charge/discharge current
- warranty and compatibility depend on correct pairing with inverter/BMS communication
- installer experience is very important

## BYD Strengths

- strong official compatibility with several premium hybrid inverter ecosystems
- common pairing with Fronius GEN24 / Symo Hybrid storage solutions
- high-voltage HVS/HVM architecture can reduce current for a given power
- compact modular tower design
- strong market reputation and certification base

## BYD Risks / Watch Points

- significantly higher price per useful kWh in many offers
- often makes most sense only when the chosen inverter ecosystem is built around it
- less attractive if the project goal is maximum openness and price/performance
- the higher cost must be justified by inverter compatibility, backup capability, warranty/service or installation simplicity

## Objective Decision Rule

Choose BYD if:

- the preferred inverter officially supports BYD much better than Pylontech
- the supplier offers a stronger complete-system warranty/service package
- high-voltage architecture is materially useful for the planned backup/power design
- the price premium is reasonable compared with the total system benefit

Choose Pylontech if:

- the preferred inverter officially supports it
- the installer has real experience with the exact inverter + Pylontech combination
- the design uses enough modules for required charge/discharge power
- local data/control integration is good
- the price difference can be used for more capacity or better infrastructure

## Current Decision For This House

The current project decision is Pylontech with Victron:

```text
3x Victron MultiPlus-II 48/5000/70-50
1x Cerbo GX Mk2
minimum 3x Pylontech US5000
target expansion to approximately 5-6x US5000
```

Deye / Sunsynk + Pylontech remains the price/performance fallback. Fronius + BYD remains the premium benchmark.

## Sources To Track

- BYD Battery-Box downloads and compatibility lists: https://www.bydbatterybox.com/downloads
- Fronius battery compatibility overview: https://www.fronius.com/en-gb/uk/solar-energy/installers-partners/technical-data/all-products/storage-units/battery-overview/battery-overview
- Pylontech US5000 downloads: https://en.pylontech.com.cn/service/downloads?id=us5000
- Pylontech rack residential ESS specs: https://www.pylontech.com.cn/products/homeess2
- Victron battery compatibility overview: https://www.victronenergy.com/live/battery_compatibility:start
- Victron + Pylontech compatibility: https://www.victronenergy.com/live/battery_compatibility:pylontech_phantom
