# Room Index

This index will become the entry point for room-by-room planning after the floor plan is available.

## Known Rooms / Areas

| Area | Status | Notes |
|---|---|---|
| Living room + kitchen + dining | expected | Main DALI lighting zone, LED square, dining spots |
| Bedroom | expected | Temperature control, possible CO2 preparation |
| Office | expected | Home office, CO2 preparation, high-quality presence detection |
| Children room 1 | expected | CO2 preparation, manual-first lighting |
| Children room 2 | expected | CO2 preparation, manual-first lighting |
| Bathroom 1 | expected | Presence detector, humidity preparation, ventilation boost |
| Bathroom 2 | expected | Presence detector, humidity preparation, ventilation boost |
| Hallway | expected | Presence detector, night lighting |
| Technical room | expected | Distribution board, KNX, network, ventilation, PV/battery area |
| Future garage | future | Presence detector, wallbox, door contact, garage door logic |
| Future covered terrace | future | Lighting, shading, preparation conduits |
| Future pool technology | future | Energy-aware, not part of backup load |
| Future garden / borehole | future | Irrigation, not part of backup load |

## Room File Naming

Use lowercase names with numeric prefixes:

```text
docs/rooms/01-living-kitchen-dining.md
docs/rooms/02-bedroom.md
docs/rooms/03-office.md
docs/rooms/04-child-room-1.md
docs/rooms/05-child-room-2.md
docs/rooms/06-bathroom-1.md
docs/rooms/07-bathroom-2.md
docs/rooms/08-hallway.md
docs/rooms/09-technical-room.md
docs/rooms/20-future-garage.md
docs/rooms/21-future-covered-terrace.md
```

## Planning Rule

Every room file should clearly separate:

- local KNX functions
- DALI lighting
- electrical preparation
- sensors
- Home Assistant additions
- open questions
