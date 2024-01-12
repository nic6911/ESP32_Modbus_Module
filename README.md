# ESP32_Modbus_Module
ESP32 modbus module intended for use with Home Assistant to support various modbus enabled devices. Currently I have used and tested:
- Nilan Ventilation with CTS602/602Light and CTS400 w. modbus
- Wavin AHC9000 floor heating
- Wavin Sentio floor heating
- EM340 electricity meter w. modbus
- NIBE F1255 heatpump (https://github.com/elupus/esphome-nibe)

There are a couple of additional code examples that has been tested and verified by users om the example code folder.

The module is not limited to those applications, but since I haven't tried other applications I give no promises !

You can buy the module here: 
https://www.ustepper.com/shop/#!/products/esphome-modbus-module

[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://bmc.link/nic6911w)

## Disclaimer
Do this at your own risk ! You are interfacing with hardware that you can potentially damage if you do not connect things as required !
Using the hardware and code presented here is done at you own risk. The hardware and software has been tested on the devices listed above without issues.

## Connecting your module

#### !! THE RJ45 INTERFACE MATCHES WAVIN AHC9000/Sentio ONLY ! 

On Wavin you simply use a patch cable (straight) and connect it from the module to the Modbus port and then you are done :)

#### SEE THE WIRING INFO BELOW FOR E.G. NILAN CONNECTION
So, taking an RJ45B cable and cutting it will leave you with colored wires that have the functions as shown below (for a RJ45B !):
![Connections](/electronics/connection.png)

Generally you need A (modbus+), B (modbus-), GND and optionally you can connect 8-24VDC to the +12V wires or you can plug in the USB-C cable from e.g., a charger to power the module. The module can consumer up to 340mA on 3.3V which for a 12V supply would be 100mA and 50mA for 24V as the module has a power converter without too much loss.

## Software + Video Guides !
The module is intended for use with Home Assistant and ESPHome though not limited to this.

See the video guide for uploading AHC9000 software to the module from your laptop using USB:
https://youtu.be/Q5KRcv-uObo

For Wavin, you need to add/delete the channels and edit names to match your setup.
The procedure for programming is the same for all code bases - Nilan, Nibe, EM340 etc...

See the video guide here on how to set it up wirelessly (Wavin Sentio example): 
https://youtu.be/s8QjRjI9TLo

### Generic Nilan code
Besides my example codes for CTS602, 602 light and CTS400 you can find generic code for all Nilan here:
https://github.com/Jopand/esphome_components/blob/main/README.md

The only board specific thing to include is:
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
Where baud rate must match your system of course - here a Nilan example.

## Connecting examples

#### A wiring example on a Nilan Comfort 300 CTS602 light is shown here:
![Connections](/electronics/CTS602_light.png)

#### A wiring example on a Nilan CTS400 is shown here:
![Connections](/electronics/CTS400_connections.png)

#### A wiring example on a EM340 modbus power meter is shown here:
![Connections](/electronics/EM340_connection.png)

#### A Nibe Heat Pump modbus interface is shown here:
![Connections](/electronics/nibe_modbus_connection.png)

#### If in doubt, look up your electric diagram or write me !

## Updated Hardware as of February 2023
The module includes:
- ESP32-C3-MINI-1 WiFi module w. 4MB flash and 400KB SRAM
- RS485 modbus interface IC
- USB-C interface for power and programming
- Switch mode buck for powering the device from any source providing 8-24VDC (USB power not required)
- 2 x optocoupler outputs
- I/O's on two pin rows
- RJ45 interface compliant with the Wavin Sentio/AHC9000 interface

The form factor and visuals is the same as for the previous ESP32-PICO. The change results in a BOM reduction and thus a price reduction due to the integrated USB controller in the C3.

The following schematic shows the details of the module:
![Schematic](/electronics/schematicsC3.png)

### Board setup from February 2023
The board dependent setup part is as follows for the ESP32-C3:
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

## Hardware pre-february 2023
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

#### !! THE RJ45 INTERFACE MATCHES WAVIN ONLY ! 

### Board setup pre-february 2023
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
