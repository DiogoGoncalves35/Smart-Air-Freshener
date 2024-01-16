# Smart Air Freshner

![Kicad](https://img.shields.io/badge/KiCad-314CB0.svg?style=for-the-badge&logo=KiCad&logoColor=white) ![ESPHOME](https://img.shields.io/badge/ESPHome-000000.svg?style=for-the-badge&logo=ESPHome&logoColor=white)  ![Home Assistant](https://img.shields.io/badge/home%20assistant-%2341BDF5.svg?style=for-the-badge&logo=home-assistant&logoColor=white) 


This board is designed to control a standard Air Freshener via ESPHome and Home Assistant, this way it's possible to automate the device by time or any condition defined.

<img src="/Images/Board_1.png">

<img src="/Images/Board_2.png">

The board fits in the same place as the default board because both have the same dimensions.

<img src="/Images/Board_3.png">

<img src="/Images/Board_4.png">

------------


### Schematic 

The [schematic](/Hardware/PCB/Schematic.pdf) is arround ESP12-E module with the basic configuration (Resistors needed), the AMS1117 regulates the 5V input voltage to 3.3V. The microcontroller controls the motor via an 2N2222 transistor and the 1N4007 diode protects the circuit in case of back voltage generated when the motor turns off.

<img src="/Images/Schematic.png">

------------

### PCB

[This](Hardware/PCB/) 1.6mm board contains 2 layers, both connected to GND, under the antenna GND area was removed. Programming connectors are SMD because it's only necessary to program the board once, after, it's possible to program over-the-air. Design it's not the best and should be improved, the only problem is related to component placement, there isn't much space to put the components on the edges.

<img src="/Images/PCB.png">

---

### ESPHome Code

This code block contains the needed code to control the air freshener. Whenever Spray button is pressed in Home Assistant, the motor turns on for a second and then turns off. With the button inside HA, it's possible to automate the device in different ways.

```
button:
  - platform: template
    name: "Spray"
    icon: "mdi:air-purifier"
    on_press:
    - switch.turn_on: motor
    - delay: 1000ms
    - switch.turn_off: motor

switch:
  - platform: gpio
    pin: GPIO4
    id: motor
```
------------

### Known issues

- None for now


------------

### To-Do

- USB-C connector ? (Better for connecting, removes need for soldering)
- Fuse protection
- SMD components





