# ESP32_Modus_Module
ESP32 modbus module intended for use with Home Assistant to support various modbus enabled devices. Currently I have used and tested:
- Nilan Ventilation with CTS602/602Light and CTS400 w. modbus
- Wavin AHC9000 floor heating
- Wavin Sentio floor heating

The module is not limited to those applications, but since I haven't tried other applications I give no promises !

## Disclaimer
Do this at your own risk ! You are interfacing with hardware that you can potentially damage if you do not connect things as required !
Using the hardware and code presented here is done at you own risk. The hardware and software has been tested on the devices listed above without issues.

## Hardware
The module includes:
- ESP32-PICO-MINI-02-N8R2 WiFi module w. 8MB flash and 2MB ram
- RS485 modbus interface IC
- USB-C interface for power and programming
- Switch mode buck for powering the device from any source providing 8-24VDC (USB power not required)
- 2 x optocoupler outputs
- I/O's on two pin rows
- RJ45 interface compliant with the Wavin Sentio/AHC9000 interface

Rendering of the module can be seen here:
![Top](/electronics/top.png)
![Bottom](/electronics/bottom.png)

The following schematic shows the details of the module:
![Schematic](/electronics/schematics.png)

#### !! THE RJ45 INTERFACE MATCHES WAVIN ONLY ! - SEE THE WIRING INFO BELOW FOR E.G. NILAN CONNECTION

On Wavin you simply use a patch cable (straight) and connect it from the module to the Modbus port and then you are done :)

A wiring example on a Comfort 300 and Wavin AHC9000 is shown here:
![Connections](/electronics/connection.png)

## Software
The module is intended for use with Home Assistant and ESPHome though not limited to this.
See the video guide here on how to set it up: 
https://youtu.be/gB1TLhx6Nzc

The board dependent setup part is as follows:
```
esphome:
  name: nilan
esp32:
  board: pico32
  framework:
    type: arduino

uart:
  rx_pin: 13
  tx_pin: 14
  parity: EVEN
  baud_rate: 19200
  id: uart_modbus
  stop_bits: 1
  
modbus:
  id: modbus_id
  flow_control_pin: 26
  uart_id: uart_modbus
```  