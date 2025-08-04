from datetime import datetime
from pathlib import Path

# Define the new content for MEM.md
today = datetime.today().strftime("%Y-%m-%d")
mem_md_content = f"""\
# ✅ MEM.md — AI_Optimized_DCM_LCR_Charging Project Memory
**Maintained by:** Kiwi-Scott  
**Purpose:** Shared long-term memory and context repository for ChatGPT across all project facets.  
**Last updated:** `{today}`

---

## 🧠 Project Index

| Facet | Description |
|-------|-------------|
| [1. Teensy Analog Scope Logger](#1-teensy-analog-scope-logger) | Teensy 4.1 firmware for signal acquisition and buffered logging |
| [2. Nano Burst Generator](#2-nano-burst-generator) | Ultra-fast, gate-safe burst generator for manual testing |
| [3. VIC/WFC Simulation & Optimization](#3-vicwfc-simulation--optimization) | Python/JS models to optimize charge accumulation in VIC5 |
| [4. Event Manager (Foster Care Tool)](#4-event-manager-foster-care-tool) | Google Sheets-based care coordination platform |
| [5. Braun–Stanley Layer](#5-braunstanley-layer) | High-impedance unidirectional junction material experiments |
| [6. Coil Winder (TeensyStep)](#6-coil-winder-teensystep) | Automated bifilar/segmented coil winder using Teensy 3.5 + DRV8825 |
| [7. User Dev Environment Setup](#7-user-dev-environment-setup) | Local config: GitHub, Jupyter, Anaconda, LTSpice, Sublime, WSL |

---

## 1. Teensy Analog Scope Logger

- **MCU:** Teensy 4.1  
- **Frontend:** Serial-based trace viewer (PC-side web UI)  
- **Channels:**
  - `BNC1` and `BNC2`: Live preview (downsampled)
  - `LOG1` and `LOG2`: Full-resolution buffered logger
- **Signal Path:**
  - Input → AMC3301 (isolated diff amp) → Teensy ADC  
  - Buffered to circular log with trigger support  
- **Status:** Live preview and logging buffer working, UI in development  
- **Repo:** https://github.com/Kiwi-Scott/Teensy_AnalogScope_Logger  
- **Todo:**
  - Logger overlay in web UI
  - Teensy firmware sync with Nano bursts
  - Zoom on logged data

---

## 2. Nano Burst Generator

- **MCU:** Arduino Nano  
- **Output:** Gated, unipolar pulse bursts (frequency + count + gateDelay)  
- **Features:**
  - Rotary encoder + button UI  
  - Clean gate between bursts (pulsingNow flag added)  
  - LCD (I2C) and OLED selectable
- **MOSFET Driver:** `Single-Isolated MOSFET Switch PCB v6.2`  
- **Status:** Working up to ~30kHz burst gating cleanly  
- **Repo:** https://github.com/Kiwi-Scott/Nano_Burst_Generator  
- **Todo:**
  - Confirm edge cleanness at full duty  
  - Confirm safe driver interface

---

## 3. VIC/WFC Simulation & Optimization

- **Sim Target:** VIC5 + Water Fuel Cell (WFC)  
- **Goals:**
  - Maximize LMD (displacement) current
  - Avoid TEM (conduction) onset
  - Optimize pulse timing + physical parameters
- **Tools:**
  - Python: `vic5_sim.py`, ESR models (Cole–Cole)
  - JavaScript: Scope simulator (HTML+JS)
  - LTSpice: VIC/LCR analog behavior
- **Key Concepts:**
  - Dynamic ESR (gap & time dependent)
  - Beating modulation from asymmetrical choke inductance
- **Repos:**
  - Main: https://github.com/Kiwi-Scott/AI_Optimized_DCM_LCR_Charging
  - Scope UI: `simulation_interface.html` (not yet in repo)
- **Status:** Phase 2 simulation active, UI expanding  
- **Todo:**
  - Improve numerical stability
  - Add Teensy-optimized simulation loop
  - Integrate scope UI with logger data

---

## 4. Event Manager (Foster Care Tool)

- **Platform:** Google Sheets + Apps Script  
- **Features:**
  - Add Event sidebar with branching logic
  - Repeat event rules (weekly, nth weekday, etc.)
  - User-based views, protections, and audit trail
- **Goal:** Transition support + compliance management  
- **Repo:** https://github.com/Kiwi-Scott/Event-Manager  
- **Notes:**
  - `MEM.md` stored here for persistent AI memory
  - UI in rollout testing phase
- **Todo:**
  - Add advanced repeat rules
  - Add onboarding and exclusion logic

---

## 5. Braun–Stanley Layer

- **Purpose:** Unidirectional junction layer for high-impedance rectification  
- **Method:**
  - Copper-plate nichrome or SS304 wire  
  - Heat with DC to Curie while exposed to sulfur  
- **Status:** Released as open-source  
- **DOI:** [10.5281/zenodo.16628395](https://doi.org/10.5281/zenodo.16628395)  
- **Repo:** https://github.com/Kiwi-Scott/Braun-Stanley-Layer  
- **Todo:**
  - Build and test electron directionality
  - Explore dielectric junction configurations

---

## 6. Coil Winder (TeensyStep)

- **MCU:** Teensy 3.5  
- **Driver:** DRV8825  
- **Purpose:** Precision bifilar/segmented winding for VIC and Attenuation TX  
- **Repo:** https://github.com/Kiwi-Scott/TeensyStep_Bobbin_Winder  
- **Based on:** `winder` and `drivers` examples by luni64  
- **Status:** Hardware ready, TeensyStep scaffolding active  
- **Todo:**
  - Customize for bifilar switching
  - Integrate auto-layer tracking

---

## 7. User Dev Environment Setup

- **Current stack:**
  - `Git for Windows`
  - `Anaconda` + `mamba`
  - `WSL2` + `Ubuntu 22.04`
  - `Jupyter Notebook` with Python & Xeus-Cling
  - `Sublime Text`
  - `LTSpice`
- **Shortcuts:**
  - `alias proj='cd ~/AI_Optimized_DCM_LCR_Charging'`
- **Common workflows:**
  - Run Jupyter inside Ubuntu:  
    ```bash
    wsl
    conda activate cling_env
    jupyter notebook
    ```
  - Push to GitHub from Git Bash:
    ```bash
    git add .
    git commit -m "msg"
    git push origin main
    ```
- **Todo:**
  - Add Arduino/Teensy platformIO support
  - Add local live plot viewer (Matplotlib or Plotly)

---

## 🔄 How to Use This File

When this file is updated:

1. Push it to GitHub:  
   ```bash
   git add docs/MEM.md  
   git commit -m "Update project memory"  
   git push origin main  
