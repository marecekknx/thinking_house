# KNX Distribution Board Equipment

## Planned Core Devices

| Function | Device | Count | Notes |
|---|---:|---:|---|
| KNX power supply | MDT STC-0960.01 | 1 | 960 mA reserve for one TP line |
| IP communication | MDT SCN-IP100.03 | 1 | IP Router Secure; more than required for one line, but acceptable |
| Non-DALI switching | MDT AKS-2016.03 | 1 | Simple lights and auxiliary outputs |
| DALI lighting | MDT SCN-DA641P.04S | 1 | DALI-2 gateway, 1 x 64 devices, integrated DALI power supply |
| Blinds | MDT JAL-0810.02 | 1 | 8 channels; 4 blinds now, 4 reserve |
| Floor heating outputs | MDT AKS-1216.03 | 1 | Controls power-contactor coils |
| Binary inputs | MDT BE-16000.02 | 1 initially | Window/door contacts and technical contacts; reserve for second unit |
| Logic | MDT SCN-LOG1.02 | 1 | Local basic logic and fallback scenes |

## Known Prices

| Device | Count | Unit Price |
|---|---:|---:|
| MDT STC-0960.01 | 1 | 243.80 EUR |
| MDT SCN-IP100.03 | 1 | 263.87 EUR |
| MDT AKS-2016.03 | 1 | 373.66 EUR |
| MDT SCN-DA641P.04S | 1 | 386.62 EUR |
| MDT JAL-0810.02 | 1 | 252.65 EUR |
| MDT AKS-1216.03 | 1 | 259.14 EUR |
| MDT BE-16000.02 | 1 | 241.43 EUR |
| MDT SCN-LOG1.02 | 1 | 130.16 EUR |

Known subtotal: 2151.33 EUR.

## Do Not Buy Yet

- second AKS-2016.03 unless non-DALI circuits exceed one actuator
- second BE-16000.02 until window/door contact count is known
- KNX universal dimmers unless required by specific non-DALI fixtures
- FVE/Modbus gateway before inverter selection
- AC gateway before air-conditioning model selection
- ventilation gateway before ventilation unit selection
