# Internshala_project




# Custom ESP32 Board with MPU-6050

A minimal custom ESP32 development board with an MPU-6050 motion sensor, designed in **EasyEDA Pro**. This project covers the schematic (Problem 1) and the PCB layout (Problem 2) of an Electronics Engineering Intern assignment.

## Features

- Programming over **USB Type-C** (CH340C USB-to-serial, BOOT and RESET buttons)
- Powered from **USB Type-C or an external battery** (Schottky diode power selection, 3.3 V LDO)
- **MPU-6050** 6-axis accelerometer and gyroscope on the I²C bus
- Only the essential components, with no extra LEDs, headers or charger

## Components

| Block | Part |
|---|---|
| Microcontroller | ESP32-WROOM-32E-N4 |
| USB connector | USB Type-C 16-pin (TYPE-C-31-M-12) |
| USB-to-serial | CH340C (SOP-16) |
| Regulator | AP2112K-3.3 |
| Power selection | 2x SS14 Schottky diodes |
| Battery input | 2-pin JST PH SMD connector |
| Sensor | MPU-6050 (QFN-24) |
| User controls | 2x tactile switches (RESET, BOOT) |
| Passives | 5.1 kΩ x2, 10 kΩ x2, 4.7 kΩ x2, 100 nF, 1 µF, 10 µF, 22 µF, 2.2 nF |

## Key Connections

| Signal | Connection |
|---|---|
| USB VBUS / Battery + | Each through an SS14 diode to the 5 V rail |
| 5 V rail | AP2112K input, which gives the 3.3 V rail |
| USB D+ / D- | CH340C D+ / D- |
| CH340C TXD / RXD | ESP32 RXD0 (GPIO3) / TXD0 (GPIO1) |
| EN | 10 kΩ pull-up, 1 µF to GND, RESET switch |
| IO0 | 10 kΩ pull-up, BOOT switch |
| MPU-6050 SDA / SCL | ESP32 GPIO21 / GPIO22, with 4.7 kΩ pull-ups |
| MPU-6050 INT | ESP32 GPIO4 |
| MPU-6050 AD0 | GND (I²C address 0x68) |

## How to Upload Code

1. Connect the board to a computer with a USB-C cable.
2. Hold the **BOOT** button, then press and release **RESET**, then release **BOOT**.
3. Upload your sketch from the Arduino IDE or PlatformIO.
4. Press **RESET** to run the program.

There is no auto-reset circuit, which keeps the part count minimal.

## Power Notes

- The 5 V rail is the source voltage minus one Schottky diode drop.
- The AP2112K input must stay below 6 V. A 4.5 to 5.5 V battery pack is the safest choice.
- A single-cell LiPo works when it is fairly full, but regulation is lost near empty.
- The board has no battery charger, so charge the battery externally.

## PCB

- 2-layer board with all components on the top layer
- Board outline of about 50 mm x 40 mm (check the exact size in EasyEDA)
- ESP32 antenna at the board edge with no copper or parts near it
- GND copper pour on the bottom layer

## Repository Contents

```
.
├── main.tex            # LaTeX report
├── assets/
│   ├── schematic.png   # Schematic screenshot
│   └── pcb.png         # PCB layout screenshot
└── README.md
```

## Tools

- EasyEDA Pro V3.2.209 (schematic and PCB)
- LaTeX (report)

## Possible Improvements

- Shrink the board further towards 35 x 25 mm
- Add DTR/RTS auto-reset transistors for one-click uploads
- Add a Li-ion charger (for example TP4056)
- Add ESD protection on the USB data lines

## Author

Your Name
