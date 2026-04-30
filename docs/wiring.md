# Wiring Guide (Raspberry Pi Pico W)

## Overview
This project connects a **4x4 membrane keypad** to a **Raspberry Pi Pico W** and drives **12 LEDs**.

- Keypad columns are inputs to the firmware scan routine via the Keypad library.
- Keypad rows are driven/scanned through dedicated GPIOs.
- Each LED anode is connected to a Pico GPIO through a **220Ω resistor**.
- LED cathodes are tied to a common GND rail.

## Components (from `diagram.json`)
- 1x Raspberry Pi Pico / Pico W (`wokwi-pi-pico`)
- 1x 4x4 membrane keypad (`wokwi-membrane-keypad`)
- 12x LEDs
  - 8x blue (labels 1..8)
  - 4x red (labels A..D)
- 12x resistors, 220Ω (LED current limiting)
- 4x resistors, 1kΩ (keypad row pull-up network to 3V3)
- Jumper wires + common GND and 3V3 rails

## GPIO Pin Mapping

### Keypad
| Keypad Signal | Pico GPIO | Firmware Array |
|---|---:|---|
| C1 | GP19 | `colPins[0]` |
| C2 | GP18 | `colPins[1]` |
| C3 | GP17 | `colPins[2]` |
| C4 | GP16 | `colPins[3]` |
| R1 | GP26 | `rowPins[0]` |
| R2 | GP22 | `rowPins[1]` |
| R3 | GP21 | `rowPins[2]` |
| R4 | GP20 | `rowPins[3]` |

### LEDs
| Logical LED | Label in diagram | Pico GPIO | Firmware index |
|---|---|---:|---:|
| LED1 | 1 | GP11 | `ledPins[0]` |
| LED2 | 2 | GP10 | `ledPins[1]` |
| LED3 | 3 | GP9  | `ledPins[2]` |
| LED4 | 4 | GP8  | `ledPins[3]` |
| LED5 | 5 | GP7  | `ledPins[4]` |
| LED6 | 6 | GP6  | `ledPins[5]` |
| LED7 | 7 | GP5  | `ledPins[6]` |
| LED8 | 8 | GP4  | `ledPins[7]` |
| LED9 | A | GP3  | `ledPins[8]` |
| LED10| B | GP2  | `ledPins[9]` |
| LED11| C | GP28 | `ledPins[10]` |
| LED12| D | GP27 | `ledPins[11]` |

## Power and Ground
- All LED cathodes are connected to a common GND node (`pico:GND.4` in the Wokwi diagram).
- Row pull-up chain (`rp1..rp4`, 1kΩ) is tied to `pico:3V3`.

## Notes and Assumptions
- The provided diagram targets `wokwi-pi-pico`; a **Pico W** is pin-compatible for these GPIOs.
- No Wi-Fi pins/peripherals are used by this firmware.
- The keypad pull-up network appears external in diagram; keep it as shown for behavior parity.
