# STM32 USB Hardware Trigger for SDR

A deterministic, USB‑controlled hardware trigger generator built on STM32 timers.  
Designed for SDR, measurement, and synchronization use cases where PC‑based timing is insufficient.

---

## Motivation

Many SDR and measurement setups rely on a PC to generate timing signals.  
However, PC‑based timing suffers from:

- USB latency and jitter
- OS scheduling and context switches
- Non‑deterministic software delays

This project moves **all timing‑critical behavior into STM32 hardware**, while keeping control on the PC.

---

## Core Idea

The PC **never toggles GPIOs directly**.

Instead:
- The PC sends timing parameters over USB
- The STM32 configures its **hardware timer**
- The timer drives the GPIO **directly via alternate function**
- The pulse is generated **entirely in hardware**

This guarantees deterministic timing independent of USB or CPU jitter.

---

## Architecture Overview



---

## Timing Model

- Timer resolution: **1 µs**
- **CCR** controls the pulse width
- **ARR** controls the total timer duration
- One‑Pulse Mode ensures a single, clean trigger

Example:
- Delay before pulse: 100 µs
- Pulse width: 10 µs
- ARR = 110
- CCR = 10

---

## USB Command Concept (WIP)

Example command from PC:
TRIGGER 100 10


The firmware:
- Validates parameters
- Programs CCR / ARR
- Arms the timer
- Hardware generates the pulse

---

## Hardware

- STM32L562 Discovery Kit
- Timer: TIM2
- Output pin: PA3 (TIM2_CH4)

---

## Why This Matters for SDR

This design allows:
- Precise external triggering
- Repeatable timing across experiments
- Synchronization with RF events
- Clean separation between control and timing

It can be used with GNU Radio, SDR++, custom Python scripts, or any SDR stack capable of sending USB commands.

---

## Project Status

- [x] Timer architecture defined
- [x] Deterministic timing model
- [ ] USB command parser
- [ ] One‑pulse trigger implementation
- [ ] Example PC script
- [ ] Documentation & timing measurements

---

## License

MIT (recommended for maximum reuse)


