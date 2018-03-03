[Indoor Agriculture Project](https://docs.google.com/document/d/1ArcZqPgIa82AwvjWtvZ9FeCffs26SfxBspnVomPGeAw/edit#) Electronics Plan

Everything is based around the Raspberry Pi, turning on the pumps, turning on the lights, turning on the solenoids is all handled by the Pi’s GPIO. Even the flow meter. Maybe some kind of header board to then talk to the rest of the peripherals. Even all control algos. Everything SMART happens on the pi all in python.

## Sensorboard

The Sensorboard is based off of the [Arduino Nano](https://store.arduino.cc/usa/arduino-nano). It has a very minimal UI to:

* Enable and disable sensors on the board

* Select the ID number for the board

* Display current sensor readings

* Calibrate sensors (Calibration factors are stored in EEPROM)

The UI is based on an:

* [8x2 Char LCD Module](https://www.digikey.com/product-detail/en/newhaven-display-intl/NHD-0208BZ-FL-YBW/NHD-0208BZ-FL-YBW-ND/1701135)

* 3 Pushbuttons

The sensorboard reports all RAW values back to the pi. These may be filtered and averaged etc, but conversion from VOLTAGE to the actual data is handled by the pi.

The connections are as follows:

### Arduino Pins

<table>
  <tr>
    <td>Pin Name</td>
    <td>Pin Function</td>
    <td>Short Name</td>
    <td>Location</td>
  </tr>
  <tr>
    <td>D2 (INT)</td>
    <td>Misc Digital Input</td>
    <td>EMDI0</td>
    <td>Screw Terminal</td>
  </tr>
  <tr>
    <td>D3
</td>
    <td>Shift Register Serial</td>
    <td>SREG_SER</td>
    <td>On Board
</td>
  </tr>
  <tr>
    <td>D4</td>
    <td>Shift Register SRCLK</td>
    <td>SREG_SRCLK</td>
    <td>On Board</td>
  </tr>
  <tr>
    <td>D5</td>
    <td>CO2 Sensor UART TX</td>
    <td>ECO2R</td>
    <td>Board Connector</td>
  </tr>
  <tr>
    <td>D6</td>
    <td>CO2 Sensor UART RX</td>
    <td>ECO2R</td>
    <td>Board Connector</td>
  </tr>
  <tr>
    <td>D7 (SDA)</td>
    <td>RGB Color Sensor I2C SDA</td>
    <td>ECSDA</td>
    <td>Board Connector</td>
  </tr>
  <tr>
    <td>D8 (SCL)</td>
    <td>RGB Color Sensor I2C SCL</td>
    <td>ECSCL</td>
    <td>Board Connector</td>
  </tr>
  <tr>
    <td>D9</td>
    <td>Load Sensor Data</td>
    <td>LSDAT</td>
    <td>On Board</td>
  </tr>
  <tr>
    <td>D10</td>
    <td>Load Sensor Clock</td>
    <td>LSCLK</td>
    <td>On Board</td>
  </tr>
  <tr>
    <td>D11 (PWM)</td>
    <td>LCD Backlight LED+</td>
    <td>OLED+</td>
    <td>On Board</td>
  </tr>
  <tr>
    <td>D12</td>
    <td>Shift Register RCLK</td>
    <td>SREG_RCLK</td>
    <td>On Board</td>
  </tr>
  <tr>
    <td>D13</td>
    <td>Voltage Divider Enable</td>
    <td>DIVEN</td>
    <td>On Board</td>
  </tr>
  <tr>
    <td>A0</td>
    <td>Mux Sig Pin</td>
    <td>MUX_SIG</td>
    <td>On Board</td>
  </tr>
  <tr>
    <td>A1</td>
    <td>Mux S0</td>
    <td>MUX_S0</td>
    <td>On Board</td>
  </tr>
  <tr>
    <td>A2</td>
    <td>Mux S1</td>
    <td>MUX_S1</td>
    <td>On Board</td>
  </tr>
  <tr>
    <td>A3</td>
    <td>Mux S2</td>
    <td>MUX_S2</td>
    <td>On Board</td>
  </tr>
  <tr>
    <td>A4</td>
    <td>Hardware I2C SDA (For External Comms)</td>
    <td>I2C_SDA</td>
    <td>Board Connector</td>
  </tr>
  <tr>
    <td>A5</td>
    <td>Hardware I2C SCL (For External Comms)</td>
    <td>I2C_SDL</td>
    <td>Board Connector</td>
  </tr>
  <tr>
    <td>A6</td>
    <td>Mux S3</td>
    <td>MUX_S3</td>
    <td>On Board</td>
  </tr>
  <tr>
    <td>A7</td>
    <td>Mux EN</td>
    <td>MUX_EN</td>
    <td>On Board</td>
  </tr>
</table>


### Multiplexer

<table>
  <tr>
    <td>Pin Name</td>
    <td>Pin Function</td>
    <td>Short Name</td>
    <td>Location</td>
  </tr>
  <tr>
    <td>I0</td>
    <td>External Temp Sensor 0</td>
    <td>ETMP0</td>
    <td>Screw Terminal</td>
  </tr>
  <tr>
    <td>I1</td>
    <td>External Temp Sensor 1</td>
    <td>ETMP1</td>
    <td>Screw Terminal</td>
  </tr>
  <tr>
    <td>I2</td>
    <td>External Temp Sensor 2</td>
    <td>ETMP2</td>
    <td>Screw Terminal</td>
  </tr>
  <tr>
    <td>I3</td>
    <td>Soil Moisture Sensor 1 </td>
    <td>ESMT0</td>
    <td>Screw Terminal</td>
  </tr>
  <tr>
    <td>I4</td>
    <td>Soil Moisture Sensor 2</td>
    <td>ESMT0</td>
    <td>Screw Terminal</td>
  </tr>
  <tr>
    <td>I5</td>
    <td>Onboard Temp Sensor 0</td>
    <td>OTMP0</td>
    <td>On Board</td>
  </tr>
  <tr>
    <td>I6</td>
    <td>Onboard LDR 0</td>
    <td>OLDR0</td>
    <td>Board Connector</td>
  </tr>
  <tr>
    <td>I7</td>
    <td>O2 Sensor</td>
    <td>BO2G0</td>
    <td>On Board</td>
  </tr>
  <tr>
    <td>I8</td>
    <td>Ambient Humidity</td>
    <td>OMST0</td>
    <td>On board</td>
  </tr>
  <tr>
    <td>I9</td>
    <td>External Turbidity 0</td>
    <td>ETRB0</td>
    <td>Board Connector</td>
  </tr>
  <tr>
    <td>I10</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>I11</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>I12</td>
    <td>External Board Detection</td>
    <td>EEBD0</td>
    <td>Board Connector</td>
  </tr>
  <tr>
    <td>I13</td>
    <td>UI Button 1 (<)</td>
    <td>OUI0</td>
    <td>On Board</td>
  </tr>
  <tr>
    <td>I14</td>
    <td>UI Button 2 (*)</td>
    <td>OUI1</td>
    <td>On Board</td>
  </tr>
  <tr>
    <td>I15</td>
    <td>UI Button 3 (>)</td>
    <td>OUI2</td>
    <td>On Board</td>
  </tr>
</table>


A sensor board that we can stick all over the cabinet to sense critical environmental data. There will be more than one of these boards through the whole design. Sensor boards are based around the arduino mini which communicates with the Raspberry Pi as a master and the arduino responds as a [slave](https://www.arduino.cc/en/Tutorial/MasterWriter). 

Should be able to detect following variables (sensors are linked as hyperlinks):

* [Onboard temperature](https://www.digikey.com/product-detail/en/ametherm/1DC103K-EC/570-1229-ND/5970118)

* [External temperature (optional through some kind of screw terminal)](https://www.adafruit.com/product/372)

* [Ambient light Level](https://www.digikey.com/products/en?dc=16426)

* [Light Color](https://www.adafruit.com/product/1334?gclid=Cj0KCQiA2Y_UBRCGARIsALglqQ1tPgwjs8Q0iPb3CzkeynlRJk4hzR49dijqtHjcTRZPo-LJaD_BfX8aAv9AEALw_wcB)

* [Ambient Moisture](https://www.digikey.com/product-detail/en/honeywell-sensing-and-productivity-solutions/HIH-4030-003/480-3167-ND/1886072)

* [Soil Moisture (external)](https://www.sparkfun.com/products/13322)

* [O2 Content](https://www.seeedstudio.com/Grove-Oxygen-Sensor%28ME2-O2-%D0%A420%29-p-1541.html)

* [CO2 Content](https://www.ebay.com/itm/New-MH-Z19B-Infrared-Carbon-Dioxide-CO2-Monitor-Sensor-Module-UART-PWM-Output/302501791946?epid=5002546034&hash=item466e8308ca:g:nwoAAOSwH-dZ8ae~:sc:USPSFirstClass!02169!US!-1)

* [Reservoir Water Turgidity](https://www.dfrobot.com/product-1394.html)

## Relays

All control is done through relays. 8 Channel Relay Module

<table>
  <tr>
    <td>12VDC Relay Bank
Relay Number
Usage
1
Plant 1 Solenoid
2
Plant 2 Solenoid
3
Mister Solenoid
4
Immersion Heater
5
Reservoir Solenoid 
6
Plant 1 Heat Mat
7
Plant 2 Heat Mat
8

</td>
    <td>120VAC Relay Bank
Relay Number
Usage
9
Grow Light 1
10
Grow Light 2
11
Grow Light 3
12
Grow Light 4
13
Grow Light 5
14
Grow Light 6
15
Heat Fan
16

</td>
  </tr>
</table>


https://www.mouser.com/ProductDetail/Microtips-Technology/NMTC-S0802XRYHS-10?qs=sGAEpiMZZMt7dcPGmvnkBodJ4P%252bCTn9wzC1sPgoRj%2fY%3d

