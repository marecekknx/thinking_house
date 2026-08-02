# Current Decisions

## House

- Bungalow, approximately 150 m2.
- Technical room will contain the main technical systems.
- Passive-standard building target.
- Fireplace will be the backup heat source in winter.

## KNX

- KNX is the local backbone of the house.
- One KNX TP line is expected to be enough.
- MDT is the preferred KNX manufacturer for core distribution-board devices.
- Home Assistant is not the primary control layer.

## Lighting

- Use a hybrid lighting design:
  - DALI for main living spaces, dimmable lights, LED strips and scenes.
  - KNX switching actuator for simple non-DALI lights and auxiliary outputs.
- One KNX switching actuator is expected to be enough if DALI is used for most lighting.
- Do not buy KNX universal dimmers unless a specific non-DALI dimmable fixture requires them.

## Heating And Cooling

- Electric floor heating, controlled by KNX outputs via power contactors.
- KNX actuator outputs should control contactor coils, not heating mats directly.
- Air conditioning is a backup for prolonged heat waves, not the primary cooling concept.
- Passive design, blinds and heat recovery ventilation are the first cooling layers.

## Ventilation

- Heat recovery ventilation should keep its own basic controller and protections.
- Prefer local Modbus TCP/RTU, local API or KNX integration.
- Home Assistant may optimize ventilation, but must not be required for safe base operation.

## Energy

- PV with battery storage is planned.
- The goal is minimum dependence on the energy supplier.
- Spot-price-based buy/sell optimization is planned.
- AI optimization may start in the cloud, but fixed limits must remain local.
- Basic backup operation for about 24 h should be possible without electric heating.

## Future Stages

- Connected garage, probably after the main house.
- Covered terrace.
- EV charging with PV-surplus preference.
- Borehole for garden irrigation and pool water.
- Pool in 1-3 years after main construction.
