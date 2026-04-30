cmake_minimum_required(VERSION 3.13)

project(pico_keypad_led_controller C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# This repository keeps the original application logic in Arduino style
# (setup/loop + Keypad library) to match Wokwi behavior exactly.
# Build on real hardware using Earle Philhower's Arduino-Pico core,
# PlatformIO, or Arduino IDE (see README).

add_custom_target(source_only ALL
  COMMENT "Documentation-first repository: use Arduino-Pico/PlatformIO to compile src/main.cpp")
