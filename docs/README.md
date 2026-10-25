---
layout: home
permalink: index.html

# Please update this with your repository name and project title
repository-name: e22_3YP_I.V.I.S
title: Smart Adaptive IoT Medical Air Bed
---

# Smart Adaptive IoT Medical Air Bed with Automated Pressure and Temperature Mapping

### Team I.V.I.S — 3rd-Year Embedded IoT Group Project
**Department of Computer Engineering, Faculty of Engineering, University of Peradeniya**  
*September 2026*

[![Department](https://img.shields.io/badge/Dept-Computer%20Engineering-blue.svg)](http://www.ce.pdn.ac.lk/)
[![University](https://img.shields.io/badge/University%20of-Peradeniya-8A2BE2.svg)](https://eng.pdn.ac.lk/)
[![Batch](https://img.shields.io/badge/Batch-E22-orange.svg)]()
[![Repository](https://img.shields.io/badge/repo-e22__3YP__I.V.I.S-181717?logo=github&logoColor=white)](https://github.com/cepdnaclk/{{ page.repository-name }})

---

## Team

- E/22/330, R. Shathursima, [email](mailto:e22330@eng.pdn.ac.lk)
- E/22/373, L. Sharmilan, [email](mailto:e22373@eng.pdn.ac.lk)
- E/22/385, S. Sulaxshan, [email](mailto:e22385@eng.pdn.ac.lk)
- E/22/193, S. Kishonithan, [email](mailto:e22193@eng.pdn.ac.lk)

---

#### Table of Contents
1. [Introduction](#introduction)
2. [Solution Architecture](#solution-architecture)
3. [Hardware and Software Designs](#hardware-and-software-designs)
4. [Safety Features & Emergency Controls](#safety-features--emergency-controls)
5. [Implementation Plan](#implementation-plan)
6. [Testing](#testing)
7. [Detailed Budget](#detailed-budget)
8. [Conclusion](#conclusion)
9. [Links](#links)

---

## Introduction

### Background & Clinical Challenge
Pressure ulcers (commonly known as **bedsores** or decubitus ulcers) represent one of the most debilitating and costly complications experienced by elderly, paralyzed, post-operative, and chronically bedridden patients. When a patient remains in a fixed position for extended periods, localized mechanical pressure over bony prominences—such as the sacrum, heels, hips, and shoulder blades—exceeds capillary blood pressure (typically 32 mmHg). This continuous load compresses capillaries, obstructs microvascular blood flow, and causes localized tissue ischemia and cellular necrosis.

Furthermore, trapped cutaneous body heat combined with perspiration elevates tissue metabolic demand while softening epidermal layers (maceration), dramatically accelerating the rate of skin breakdown.

```
+-----------------------------------------------------------------------------------+
|                            Bedsore Causation Cycle                                |
|                                                                                   |
|  [ Prolonged Immobility ]  -->  [ Continuous Local Pressure (> 32 mmHg) ]         |
|                                                     |                             |
|                                                     v                             |
|  [ Trapped Body Heat & Moisture ] --> [ Microvascular Blood Flow Cutoff ]         |
|                 |                                   |                             |
|                 v                                   v                             |
|  [ Accelerated Skin Maceration ]  -->  [ Tissue Ischemia & Ulcer Formation ]      |
+-----------------------------------------------------------------------------------+
```

### Limitations of Existing Alternatives
1. **Standard Alternating Pressure Mattresses:** Available consumer and hospital air mattresses operate purely on dumb, fixed-time duty cycles (e.g., alternating rows every 10–15 minutes). They possess **no sensory awareness** of patient posture, localized pressure hot-spots, or cutaneous heat build-up.
2. **Commercial Smart Beds:** High-end clinical ICU beds with pressure mapping exist in the global market, but their astronomical cost (ranging from $10,000 to $40,000) places them entirely out of reach for developing healthcare systems, regional hospitals, and home-care settings.
3. **Manual Caregiver Turning:** Clinical guidelines recommend manually repositioning bedridden patients every two hours. However, severe nursing staff shortages cause missed turns, chronic caregiver fatigue, and inconsistent patient outcomes.

### Our Solution: Team I.V.I.S
**Team I.V.I.S** is engineering an affordable, intelligent, closed-loop medical air bed overlay that integrates real-time pressure distribution and temperature mapping with dynamic pneumatic chamber regulation. By continuously monitoring patient touchpoints across critical vulnerability zones, our system relieves pressure points autonomously, dissipates heat, and transmits live telemetry to an interactive caregiver dashboard.

---

## Solution Architecture

The I.V.I.S system adopts a modular, 3-tier IoT architecture integrating sensory acquisition, intelligent edge actuation, and wireless cloud telemetry.

```
+-----------------------------------------------------------------------------------+
| 1. SENSOR MATRIX TIER (Mattress Overlay)                                          |
|    - High-density Force Sensitive Resistor (FSR) Grid Array                       |
|    - Zoned Digital Temperature Sensor Network                                     |
|    - Target Zones: Head, Torso / Scapulae, Sacrum / Pelvis, Lower Limbs / Heels   |
+------------------------------------------+----------------------------------------+
                                           | Multi-Channel ADC / Multiplexed Bus
                                           v
+-----------------------------------------------------------------------------------+
| 2. SMART EMBEDDED CONTROL & ACTUATION TIER                                        |
|    - Central Microcontroller (ESP32 Edge Gateway)                                 |
|    - Real-Time Calibration & Moving-Average Filtering                             |
|    - Adaptive Zoned Pressure-Relief Algorithm                                     |
|    - Pneumatic Driver: 12V DC Compressor Pump + Solenoid Valve Manifold           |
|    - Safety Locks: Power-Loss Air Retention & Emergency CPR Hardening Mode        |
+-------------------+---------------------------------------+-----------------------+
                    |                                       |
     Pneumatic Air  |                                       | Wi-Fi (MQTT / HTTP)
     Distribution   v                                       v
+---------------------------------------+   +---------------------------------------+
| Multi-Chamber Inflatable Mattress     |   | 3. LIVE MONITORING & TELEMETRY TIER   |
| - Independent Anatomical Bladders     |   | - Caregiver Web/Mobile Dashboard      |
| - Rapid Inflate / Deflate Venting     |   | - Real-time Pressure & Heat Heatmaps  |
| - Automatic Pressure Equalization     |   | - High-Risk Patient Inactivity Alerts |
+---------------------------------------+   +---------------------------------------+
```

### System Workflow
1. **Continuous Sensory Scanning:** The multiplexed sensor matrix scans localized pressure and temperature values across the mattress overlay at predetermined intervals.
2. **Edge Matrix Processing:** The microcontroller aggregates readings, converts analog resistance variations into pressure equivalents, and compares values against safe clinical thresholds (e.g., sustained pressure > 30 mmHg or temperatures > 36.5 °C).
3. **Closed-Loop Zoned Redistribution:** When prolonged pressure or heat accumulation is detected in an anatomical zone (such as the sacrum), the control unit activates the corresponding exhaust valve to reduce chamber pressure while gently increasing pressure in adjacent zones to balance patient support.
4. **Caregiver Telemetry:** Live pressure and temperature matrices are packaged into lightweight JSON payloads and streamed via MQTT to the caregiver dashboard for continuous visualization.

---

## Hardware and Software Designs

### Hardware Design

The hardware infrastructure is engineered for medical safety, low acoustic noise, and cost efficiency.

```
+-----------------------------------------------------------------------------------+
|                            Hardware Block Diagram                                 |
|                                                                                   |
|  [ 12V 5A Medical Power Supply ] ---> [ Buck Converters (5V / 3.3V) ]             |
|                                           |                                       |
|  +----------------------------------------+------------------------------------+  |
|  |                                                                             |  |
|  v                                                                             v  |
|  [ ESP32 MCU Node ] <======== [ 16-Ch MUX CD74HC4067 ] <=== [ FSR Matrix Array ]  |
|         |           <======== [ One-Wire Bus ] <=========== [ DS18B20 Temp Array] |
|         |                                                                         |
|         +-------------------+--------------------+                                |
|         | (GPIO)            | (PWM / GPIO)       | (Interrupt Input)              |
|         v                   v                    v                                |
|  [ Relay / MOSFET Driver ]  [ 12V Silent Pump ]  [ Emergency CPR Button ]         |
|         |                                                                         |
|         v                                                                         |
|  [ Solenoid Valve Manifold (Ch 1 - 4) ] ===> [ Multi-Zone Air Bladders ]          |
+-----------------------------------------------------------------------------------+
```

#### 1. Sensor Matrix Subsystem
* **Pressure Sensors:** Matrix of Force Sensitive Resistors (FSRs) integrated onto a flexible backing layer. Resistor values decrease non-linearly with applied mechanical force, mapped through voltage divider circuits and high-speed CD74HC4067 16-channel analog multiplexers.
* **Temperature Sensors:** Digital DS18B20 probes wired on a 1-Wire communication bus, calibrated to read cutaneous interface temperatures with 0.1 °C resolution.
* **Zoned Division:** Four dedicated anatomical zones:
  - **Zone 1:** Head & Cervical Spine
  - **Zone 2:** Torso & Scapular region
  - **Zone 3:** Sacrum & Pelvic region *(Highest ulcer prevalence zone)*
  - **Zone 4:** Calves & Heels *(Critical high-vulnerability zone)*

#### 2. Pneumatic Actuation & Control
* **Compressor Pump:** Low-vibration, low-noise 12V DC diaphragm air pump equipped with vibration dampers for quiet bedside operation.
* **Valves & Manifold:** Miniature 2-way and 3-way 12V normally-closed (NC) solenoid valves allowing selective intake, hold, and exhaust functions for each air chamber.
* **Switching Circuits:** Optoisolated relay arrays and logic-level N-channel MOSFET drivers (IRLZ44N) driven by microcontroller GPIOs with flyback diode protection.

---

### Software Design

The software architecture is divided into embedded firmware and the caregiver interface.

```
+-----------------------------------------------------------------------------------+
|                            Software Pipeline                                      |
|                                                                                   |
|  [ Sensor Acquisition ]  --> [ Matrix Calibration & Moving Average Filtering ]    |
|                                                     |                             |
|                                                     v                             |
|  [ Telemetry Packaging ] <--- [ Closed-Loop Zoning & Redistribution Algorithm ]   |
|         |                                           |                             |
|         v                                           v                             |
|  [ MQTT over Wi-Fi ]                 [ Valve Actuation & Pump Scheduling ]        |
|         |                                                                         |
|         v                                                                         |
|  [ Caregiver Dashboard: Heatmaps, Graphs, Alarms, Emergency Override Controls ]   |
+-----------------------------------------------------------------------------------+
```

#### 1. Embedded Firmware (ESP32)
* **Real-Time Task Scheduling:** Implemented in C/C++ on FreeRTOS with separated threads for sensor polling, pneumatic state-machine control, safety monitoring, and network telemetry.
* **Calibration & Filtering:** Moving average filter and moving median filter to eliminate patient movement artifacts and electrical noise.
* **Adaptive Relieving State Machine:** Detects sustained high-pressure thresholds (> 45 minutes continuous focal loading) and activates zoned alternate-relief duty cycles.

#### 2. Caregiver Live Dashboard
* **Dynamic Heatmap Visualization:** 2D interactive canvas rendering real-time heatmaps for both pressure load and temperature distribution.
* **Threshold Alerts & Notifications:** Audio-visual alarms triggered when patient pressure spots remain unrelieved beyond safe thresholds.
* **Audit Logging:** Historical event log documenting patient turns, pressure cycles, and system events for clinical record keeping.

---

## Safety Features & Emergency Controls

Patient safety is the fundamental design criteria of the I.V.I.S bed:

| Safety Feature | Mechanism & Implementation | Clinical Purpose |
| :--- | :--- | :--- |
| **Power-Loss Air Retention Lock** | Normally Closed (NC) solenoid valves automatically lock in place if primary power or DC adapter fails. | Prevents sudden deflation of the mattress, ensuring the patient remains safely suspended on trapped air until power is restored. |
| **Emergency CPR Fast-Firm Mode** | Dedicated prominent physical latching emergency button and remote dashboard trigger. | Instantly energizes the air pump to 100% duty cycle and opens all inlet valves to make the bed completely rigid within seconds, allowing medical staff to administer CPR chest compressions. |
| **Mechanical Overpressure Relief** | Calibrated pop-off spring relief valve on the main air rail. | Ensures pneumatic lines cannot exceed safe working pressure (120 mmHg) even in the event of firmware faults. |
| **Acoustic Low-Noise Operation** | Rubber dampening mounts and acoustic enclosure for the pump unit. | Preserves patient sleep quality and prevents agitation in clinical wards. |

---

## Implementation Plan

A comprehensive 5-month milestone roadmap structured to deliver a fully functional, clinically validated prototype:

```
Month 1: [ System Architecture & Hardware Sourcing ]
Month 2: [ Sensor Array Assembly & Calibration ]
Month 3: [ Pneumatics & Actuation Assembly ]
Month 4: [ Firmware & Closed-Loop Control ]
Month 5: [ Dashboard Integration & Clinical Testing ]
```

* **Month 1: System Design, Circuit Planning & Component Gathering**
  - Finalize pneumatic piping diagrams, voltage divider multiplexer schematics, and PCB layouts.
  - Procure microcontrollers, FSR arrays, digital temperature sensors, air pump, and solenoid valves.
* **Month 2: Sensor Array Fabrication & Calibration**
  - Assemble flexible sensor matrix across anatomical zones (Head, Torso, Sacrum, Heels).
  - Calibrate FSR resistance-to-weight curves using standard calibration weights; integrate multi-channel ADC.
* **Month 3: Pneumatic Actuation & Valve Circuit Assembly**
  - Fabricate air manifold, connect solenoid valves, and wire MOSFET/relay driver stages.
  - Test airtightness, inflation/deflation timings, and power-loss fail-safe valve retention.
* **Month 4: Firmware Programming & Closed-Loop Control Logic**
  - Develop FreeRTOS firmware routines on ESP32 for continuous sensory processing.
  - Implement adaptive pressure redistribution algorithms, threshold checks, and CPR override switch logic.
* **Month 5: Live Dashboard Telemetry, Final Integration & Testing**
  - Connect MQTT broker to caregiver web dashboard and implement live visual heatmaps.
  - Conduct full-system endurance testing, simulate patient postures, and finalize project presentation.

---

## Testing

A systematic test suite will validate performance across mechanical, electrical, firmware, and telemetry tiers:

```
+-----------------------------------------------------------------------------------+
|                                 Testing Matrix                                    |
+----------------------+---------------------------------+--------------------------+
| Subsystem            | Test Objective                  | Acceptance Criteria      |
+----------------------+---------------------------------+--------------------------+
| Sensor Matrix        | Weight sensitivity & linearity  | Linear response 0–100 kg |
| Temperature Array    | Accuracy against medical probe  | Error within +/- 0.2 °C  |
| Pneumatics & Valves  | Inflation / Deflation response  | Chamber cycle < 30 s     |
| Fail-Safe Cutout     | Abrupt AC power disconnection   | > 4 hrs air retention    |
| Emergency CPR Mode   | Time to achieve rigid surface   | Rigid bed in < 15 s      |
| IoT Dashboard        | Telemetry latency over Wi-Fi    | Latency < 1.0 second     |
+----------------------+---------------------------------+--------------------------+
```

1. **Sensor Calibration Testing:** Standard known test loads applied across individual FSR cells to calibrate the ADC lookup table and eliminate sensor hysteresis.
2. **Pneumatic Leak & Retention Test:** Chambers inflated to maximum operating pressure and monitored over 12 hours to verify zero audible or measurable pressure decay.
3. **Emergency CPR Response Test:** Time elapsed from CPR button press to full chamber firmness measured to verify compliance with resuscitation guidelines.
4. **Endurance & Heat Dissipation Testing:** Running pump and valve switching continuously over 48 hours to evaluate thermal safety and component reliability.

---

## Detailed Budget

The preliminary estimated bill of materials (BOM) for prototyping the I.V.I.S medical air bed:

| Item | Component Description | Quantity | Unit Cost (LKR) | Total Cost (LKR) |
| :--- | :--- | :---: | :---: | :---: |
| 1 | ESP32-WROOM-32 Development Board | 1 |to be updated | to be updated |
| 2 | Force Sensitive Resistors (FSR Matrix Cells) | 16 |to be updated | to be updated |
| 3 | DS18B20 Waterproof Digital Temperature Sensors | 4 | to be updated | to be updated |
| 4 | CD74HC4067 16-Channel Analog Multiplexer Modules | 2 | to be updated | to be updated |
| 5 | 12V DC Ultra-Quiet Medical Micro Air Pump | 1 | to be updated | to be updated |
| 6 | 12V Normally Closed (NC) Miniature Solenoid Valves | 6 | to be updated| to be updated |
| 7 | 8-Channel Relay Module with Optocoupler Isolation | 1 | to be updated | to be updated |
| 8 | Multi-Chamber Medical Air Bed Bladder Overlay | 1 | to be updated | to be updated |
| 9 | 12V 5A Medical Grade Power Adapter & Regulators | 1 | to be updated | to be updated |
| 10 | Emergency CPR Latching Switch & Enclosure Hardware | 1 | to be updated | to be updated|
| 11 | Silicone Pneumatic Tubing, T-Connectors & Manifold | 1 |  to be updated    |to be updated|
| 12 | Custom PCB Fabrication, Terminal Blocks & Wire Harness | 1 | to be updated | to be updated|
 

---

## Conclusion

Pressure ulcers represent a widespread, painful, and costly healthcare challenge that is entirely preventable with timely pressure relief and microclimate management. While existing solutions are either unaffordable high-end clinical equipment or ineffective timer-based mattresses, **Team I.V.I.S** bridges this gap by introducing an accessible, IoT-connected smart medical air bed.

By synthesizing real-time pressure mapping, cutaneous thermal tracking, adaptive pneumatic redistribution, and critical emergency safeguards (Power Loss Lock and CPR Fast-Firm Mode), the I.V.I.S bed delivers proactive clinical-grade patient protection at an affordable fabrication cost.

---

## Links

- [Project Repository](https://github.com/cepdnaclk/e22-3YP-I.V.I.S)
- [Project Documentation Site](https://cepdnaclk.github.io/e22-3YP-I.V.I.S) 
- [Department of Computer Engineering](http://www.ce.pdn.ac.lk/) 
- [Faculty of Engineering, University of Peradeniya](https://eng.pdn.ac.lk/) 
