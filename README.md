# ESP32 Modbus Module

## Overview

The ESP32 Modbus module is designed for integrating Modbus-enabled devices with Home Assistant. It supports various devices including:

- **Nilan Ventilation** (CTS602/602Light and CTS400 with Modbus)
- **Wavin AHC9000** (Floor heating)
- **Wavin Sentio** (Floor heating)
- **EM340** (Electricity meter with Modbus)
- **NIBE F1255** (Heatpump)

The module is flexible and can be adapted for other Modbus applications, although no promises are made for unsupported devices.

[Buy the module here](https://www.ustepper.com/shop/#!/products/esphome-modbus-module)

---

## Disclaimer

**Use at your own risk!** Improper connections could potentially damage hardware. The hardware and software have been tested with the listed devices without issues.

---

## Features

- Modbus communication with popular home automation systems (e.g., **Home Assistant**, **ESPHome**).
- Supports multiple devices (Nilan, Wavin, EM340, NIBE, and more).
- Provides wiring and software guides to get started quickly.

---

## Connecting the Module

### Compatibility Notes

- **RJ45 Interface**: Works specifically with Wavin AHC9000/Sentio.
- Use a **patch cable** to connect the module to the Modbus port for these devices.

### Wiring Information

To connect the module, use an **RJ45B** cable. Cut the cable to expose colored wires, which serve the following functions:

- **A (Modbus+)**
- **B (Modbus-)**
- **GND**
- **+12V (optional)** for power, or use a **USB-C** cable from a charger.

![Connections](/electronics/connection.png)

#### A wiring example on a Nilan Comfort 300 CTS602 light is shown here:
![Connections](/electronics/CTS602_light.png)

#### A wiring example on a Nilan CTS400 is shown here:
![Connections](/electronics/CTS400_connections.png)

#### A wiring example on a EM340 modbus power meter is shown here:
![Connections](/electronics/EM340_connection.png)

#### A Nibe Heat Pump modbus interface is shown here:
![Connections](/electronics/nibe_modbus_connection.png)

---

## Software Guides

### Installation & Setup

- **Home Assistant & ESPHome**: The module integrates seamlessly with these platforms.
- [Video Guide: USB Upload for AHC9000](https://youtu.be/Q5KRcv-uObo)
- [Video Guide: Wireless Setup for Wavin Sentio](https://youtu.be/s8QjRjI9TLo)

### Example Code

You can find example code for **Nilan**, **Nibe**, **EM340**, and more in the code folder. A generic setup for **Nilan** is available [here](https://github.com/Jopand/esphome_components/blob/main/README.md).

Example configuration for **Nilan**:

```
esphome:
  name: nilan
esp32:
  board: esp32-c3-devkitm-1
  framework:
    type: arduino

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
  output_power: "8.5"

uart:
  rx_pin: 20
  tx_pin: 21
  parity: EVEN
  baud_rate: 19200
  id: uart_modbus
  stop_bits: 1
  
modbus:
  id: modbus_id
  flow_control_pin: 10
  uart_id: uart_modbus

```

