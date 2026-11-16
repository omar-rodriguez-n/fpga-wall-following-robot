# Autonomous wall-following robot on a Nexys A7 FPGA

A robot with four DC (direct current) motors, controlled entirely by digital logic written in VHDL (Very High Speed Integrated Circuit Hardware Description Language) on an FPGA (field-programmable gate array). It follows the wall on its left at 20 cm and turns right when it finds an obstacle in front.

## Hardware

| Part | Model |
|---|---|
| FPGA board | Digilent Nexys A7-100T (Artix-7 XC7A100T) |
| Motors | Four DC motors |
| Motor drivers | L298N and DBH-12V H-bridges |
| Front sensor | HY-SRF05 ultrasonic |
| Left sensor | HC-SR04 ultrasonic |

## Behavior

- Keeps the left wall at 20 cm.
- Turns right when the front sensor detects an obstacle.
- Adjusts speed by distance zones using PWM (pulse-width modulation).
- Boots on its own from the board's SPI (Serial Peripheral Interface) flash, with no computer connected.

## Key design fixes

- **Metastability:** external sensor signals are synchronized to the system clock before use.
- **Distance scaling:** corrected the conversion from echo time to centimeters (`DIV_58` = 2900).
- **Bad readings:** each sensor has its own valid signal, and filters over consecutive readings reject bad measurements.
- **Speed control:** PWM speed zones based on distance.

## Repository layout

```
src/            VHDL modules
constraints/    pin constraints (.xdc)
docs/           block diagram, photos, video
```

<!-- TODO: upload your .vhd files to src/ and your .xdc file to constraints/. -->
<!-- TODO: add a short video or GIF of the robot following the wall to docs/ and link it here. -->

## Build

Built with Vivado. The bitstream is written to the SPI flash so the robot starts when powered.

<!-- TODO: Vivado version and the exact steps you used to program the flash. -->
