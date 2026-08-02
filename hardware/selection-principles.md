# Hardware Selection Principles

## Default Questions

Every new device should pass these questions:

1. Does it work without internet?
2. Does it work without Home Assistant?
3. Does it expose a local or open interface?
4. Can it be serviced or replaced without destroying finished construction?
5. Does it fit the architecture instead of adding a parallel ecosystem?

## Preferred Interfaces

- KNX
- DALI-2
- Modbus TCP
- Modbus RTU
- MQTT
- local HTTP API
- RTSP/ONVIF for cameras
- Ethernet for fixed devices

## Avoid For Infrastructure

- cloud-only devices
- Wi-Fi-only fixed equipment when Ethernet is practical
- battery sensors where wired preparation is available
- closed ecosystems without export/control path
- devices that require Home Assistant for basic operation
