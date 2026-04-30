# Architecture

## Repository Layout

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

## Firmware Structure (`src/main.cpp`)

The source is intentionally preserved to keep original behavior.

1. **Configuration constants**
   - `LEDS = 12`, `ROWS = 4`, `COLS = 4`

2. **Lookup tables**
   - `keys[4][4]` keypad character map
   - `ledPins[12]` LED GPIO map
   - `rowPins[4]`, `colPins[4]` keypad GPIO maps

3. **Peripheral object**
   - `Keypad keypad(...)` using `Keypad` library matrix scanner

4. **`setup()`**
   - Initializes all LED GPIOs as outputs
   - Forces all LEDs OFF at boot

5. **`loop()`**
   - Reads key event with `keypad.getKey()`
   - Executes switch-case action map:
     - `1..8`: set corresponding blue LED ON
     - `9`: turn ON blue LED bank (`ledPins[0..7]`)
     - `0`: turn OFF blue LED bank
     - `A..D`: set corresponding red LED ON
     - `*`: turn ON all red LEDs (`ledPins[8..11]`)
     - `#`: turn OFF all red LEDs
   - `delay(10)` provides a short scan interval

## Behavior Guarantees
- No core logic rewrites were performed.
- Key-to-LED behavior and pin maps match the supplied code.
- Documentation and folder structure were added for maintainability.

## Portability Notes
- Code style is Arduino-compatible C++ (not raw Pico SDK API calls).
- For physical Pico W deployment, use Arduino-Pico core or PlatformIO for the cleanest path.
