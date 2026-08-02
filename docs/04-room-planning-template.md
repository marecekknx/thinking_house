# Room Planning Template

Use this template for every room once the floor plan is available.

## Room

- Name:
- Area:
- Floor:
- Main use:
- Occupancy pattern:

## Floor Plan Notes

- Doors:
- Windows:
- External blinds:
- Furniture assumptions:
- Special constraints:

## Lighting

### DALI

- DALI groups:
- DALI drivers:
- Driver location:
- Service access:
- Scenes:

### Non-DALI

- Switched circuits:
- Auxiliary outputs:
- Notes:

## Controls

- Button locations:
- Button type:
- Short press functions:
- Long press functions:
- Scene buttons:
- Manual fallback requirements:

## Sensors

- Presence detector:
- Temperature:
- Humidity:
- CO2:
- Window/door contacts:
- Other sensors:

## Heating

- Heating zone:
- Room temperature source:
- Floor temperature probe:
- Floor temperature limit:
- Heating priority:
- Fail-safe behavior:

## Cooling

- AC coverage:
- Cooling setpoint behavior:
- Blocking with heating:
- Window-open behavior:

## Ventilation

- Normal mode:
- Boost trigger:
- Humidity/CO2 trigger:
- Away/Night behavior:

## Blinds / Shading

- Blind channels:
- Manual control:
- Automatic shading:
- Wind/rain protection:
- Door/window blocking:

## Security

- Alarm role:
- Motion/presence use:
- Door/window contact use:
- Camera coverage:

## Network / Low Voltage

- Ethernet outlets:
- Wi-Fi coverage:
- Camera cable:
- Audio/video:
- Spare conduits:

## Home Assistant

- Dashboard controls:
- Non-critical automations:
- Notifications:
- Energy-aware behavior:

## KNX Mapping

- Physical devices:
- Group addresses:
- DALI groups:
- Actuator channels:
- Binary input channels:

## Open Questions

- TBD:

## Acceptance Criteria

- Basic room control works without Home Assistant.
- Manual fallback exists for all important actions.
- Drivers and technical devices remain service-accessible.
- All cables are documented in the cable book.
