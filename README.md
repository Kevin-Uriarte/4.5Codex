# Pico W Keypad-to-LED Controller

A Raspberry Pi Pico W project that reads a **4x4 matrix keypad** and controls **12 individual LEDs** based on key presses.

> Core logic is preserved exactly from the provided source; this repository focuses on clean structure and deployment documentation.

## Features
- 4x4 keypad scanning via `Keypad` library
- 12 independent LED outputs
- Single-key and group control commands:
  - `1..8` => turn ON matching blue LED
  - `9` => turn ON all blue LEDs (1..8)
  - `0` => turn OFF all blue LEDs
  - `A..D` => turn ON matching red LED
  - `*` => turn ON all red LEDs (A..D)
  - `#` => turn OFF all red LEDs

## Repository Structure

```text
.
├── CMakeLists.txt
├── README.md
├── include/
├── src/
│   └── main.cpp
└── docs/
    ├── architecture.md
    └── wiring.md
```

## Hardware Summary
See full mapping in [`docs/wiring.md`](docs/wiring.md).

- 1x Raspberry Pi Pico W
- 1x 4x4 membrane keypad
- 12x LEDs + 12x 220Ω resistors
- 4x 1kΩ resistors for keypad pull-up chain

## Build / Flash Options

### Option A (Recommended): Arduino IDE with Arduino-Pico core
Because the source uses `Keypad.h` and Arduino `setup()/loop()`, this is the most direct route.

1. Install Arduino IDE.
2. Install **Raspberry Pi Pico/RP2040** board package (Arduino-Pico by Earle Philhower).
3. Install `Keypad` library from Library Manager.
4. Open `src/main.cpp` (or copy content into an Arduino sketch).
5. Select board **Raspberry Pi Pico W**.
6. Put Pico W in BOOTSEL mode and upload.

### Option B: PlatformIO
1. Create a PlatformIO environment for `raspberrypi` platform + `rpipicow` board.
2. Set framework to `arduino`.
3. Add dependency `Keypad`.
4. Use `src/main.cpp` as-is.
5. Build/upload via PlatformIO tasks.

### About `CMakeLists.txt`
A minimal top-level `CMakeLists.txt` is included to standardize repository layout for C/C++ projects. This codebase is Arduino-framework logic, so compilation is expected through Arduino-compatible tooling (Arduino IDE/PlatformIO).

## Run in Wokwi
1. Create a new Raspberry Pi Pico project in Wokwi.
2. Replace diagram with the provided `diagram.json` content.
3. Use the firmware logic from `src/main.cpp`.
4. Start simulation and press keypad buttons to observe LED state changes.

## Run on Real Hardware (Pico W)
1. Wire hardware per [`docs/wiring.md`](docs/wiring.md).
2. Verify all LED series resistors are 220Ω and LED polarity is correct.
3. Flash firmware via Arduino IDE or PlatformIO.
4. Test keys in this order: `1`, `9`, `0`, `A`, `*`, `#`.

## Wi-Fi / Credentials
- This firmware does **not** use Wi-Fi.
- No credentials are required or stored.
- If Wi-Fi is added later, use a separate local config file (ignored by Git) and never hardcode secrets.

## Validation Checklist
- [ ] Keypad rows/columns mapped exactly as in source arrays
- [ ] LED GPIO map matches `ledPins[]`
- [ ] Common GND shared by all LED cathodes
- [ ] Pull-up network tied to 3V3

