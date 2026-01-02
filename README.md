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

