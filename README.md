# Smart Adaptive IoT Medical Air Bed with Automated Pressure and Temperature Mapping

[![Department](https://img.shields.io/badge/Dept-Computer%20Engineering-blue.svg)](http://www.ce.pdn.ac.lk/)
[![University](https://img.shields.io/badge/University%20of-Peradeniya-8A2BE2.svg)](https://eng.pdn.ac.lk/)
[![Batch](https://img.shields.io/badge/Batch-E22-orange.svg)]()
[![Course](https://img.shields.io/badge/3YP-Embedded%20IoT%20Project-success.svg)]()
[![Repository](https://img.shields.io/badge/repo-e22__3YP__I.V.I.S-181717?logo=github&logoColor=white)](https://github.com/cepdnaclk/e22_3YP_I.V.I.S)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> **3rd-Year Embedded Systems and IoT Project (3YP)**  
> **Department of Computer Engineering, Faculty of Engineering, University of Peradeniya**  
> **Team I.V.I.S** — *September 2026*

---

## 📌 Abstract

Long-term bedridden patients in hospitals, hospices, and home-care settings face severe risks of **pressure ulcers (bedsores)** and tissue breakdown caused by continuous localized body weight and trapped cutaneous heat. Existing commercial smart hospital beds are prohibitively expensive for widespread clinical adoption, while conventional consumer-grade alternating air mattresses operate blindly on dumb, fixed-interval timers without feedback regarding localized pain, tissue loading, or microclimate temperatures.

**Team I.V.I.S** proposes an affordable, intelligent medical air bed overlay driven by an automated array of pressure and temperature sensors. By mapping patient weight distribution and microclimate heat spots across key anatomical vulnerability zones in real time, the system dynamically actuates individual pneumatic chambers to alleviate high-pressure regions, dissipate trapped heat, and safeguard patient skin integrity without requiring constant manual caregiver intervention.

---

## 🎯 The Problem & Our Proposed Solution

### ⚠️ The Problem
* **Ischemic Tissue Necrosis:** Prolonged continuous pressure on sensitive anatomical bony prominences (sacrum, heels, scapulae, and back) compresses capillaries, cutting off microvascular blood perfusion.
* **Thermal Maceration:** Trapped body heat combined with perspiration creates high humidity and elevates tissue metabolic demand, accelerating skin breakdown.
* **Limitations of Existing Beds:** Standard alternating air mattresses cycle air chambers on rigid, pre-programmed timers without any physiological awareness of patient posture, actual pressure concentration, or dermal heat buildup. High-end ICU sensor beds, on the other hand, cost thousands of dollars, making them inaccessible to local clinics and home-care environments.

### 💡 Our Solution (Team I.V.I.S)
We are developing an intelligent, closed-loop adaptive air mattress overlay equipped with:
1. **Multimodal Sensory Mapping:** A continuous matrix of pressure and temperature sensors detecting contact points and thermal spikes across anatomical zones (Head, Torso, Sacrum, and Heels).
2. **Automated Dynamic Air Chamber Regulation:** Microcontroller-driven solenoid valves and mini pneumatic pumps dynamically inflate and deflate zoned air bladders to relieve identified pressure peaks.
3. **Caregiver Telemetry Dashboard:** A low-latency wireless interface providing clinicians with real-time heatmaps, posture diagnostics, and threshold alert notifications.

---

## ⚙️ How the Smart System Works

The system architecture is structured into three coordinated subsystems:

```
+-----------------------------------------------------------------------------------+
|                           Smart Sensor Matrix Layer                               |
|   [FSR Pressure Grid Array]            [Digital Body Temperature Sensors]         |
|   (Zones: Head, Torso, Sacrum, Heels)  (Zones: Core Back, Sacrum, Lower Limbs)    |
+------------------------------------------+----------------------------------------+
                                           | (Analog / I2C Bus)
                                           v
+-----------------------------------------------------------------------------------+
|                        Embedded Control & Actuation Unit                          |
|                     [Microcontroller: ESP32 / STM32 Edge]                         |
|   * Sensor Calibration & Matrix Scanning  * Real-time Body Weight & Heat Mapping  |
|   * Threshold & Posture Detection         * Closed-Loop Pneumatic Control Logic   |
|   * Power Loss Fail-Safe Lockout          * Emergency CPR Fast-Firm Control       |
+-------------------+---------------------------------------+-----------------------+
                    |                                       |
    (PWM & GPIO)    v                                       v   (Wi-Fi / MQTT / HTTP)
+---------------------------------------+   +---------------------------------------+
|        Pneumatic Actuator Unit        |   |         IoT Cloud & Dashboard         |
|  - Silent 12V Air Pump / Compressor   |   |  - Live Pressure & Thermal Heatmap    |
|  - Solenoid Valves (Inflate/Deflate)  |   |  - Threshold Alerts & Notifications   |
|  - Multi-Zone Air Bladders (4 Zones)  |   |  - Historical Logging for Clinicians  |
+---------------------------------------+   +---------------------------------------+
```

1. **Smart Sensor Matrix:**
   - Pressure sensors (Force Sensitive Resistors) detect contact points and load concentration under the patient.
   - Temperature sensor arrays monitor thermal accumulation between the mattress and patient tissue.
   - Zoned layout targeted at high-risk decubitus ulcer regions: **Head**, **Torso**, **Sacrum**, and **Heels**.

2. **Smart Control Unit:**
   - High-performance embedded microcontroller processes sensor matrix inputs.
   - Closed-loop control algorithm determines high-pressure/high-temperature thresholds.
   - Actuates relay drivers and solenoid valves to deflate high-pressure bladders while inflating neighboring support bladders to redistribute body load smoothly.

3. **Live Monitoring Dashboard:**
   - Telemetry streams via MQTT/WebSockets to a web/mobile dashboard.
   - Caregivers view real-time visual heatmaps of pressure distribution and bed temperatures.
   - Configurable alarms alert staff if a patient remains in an uncorrected high-pressure state for extended periods.

---

## 🚨 Safety Features & Emergency Controls

* 🔒 **Power Loss Safety Lock:**  
  Equipped with normally closed (NC) fail-safe valves that automatically seal all air chambers when main power drops. This prevents sudden deflation and maintains patient support until power is restored.
* ⚡ **Emergency CPR Mode:**  
  A dedicated high-priority emergency hardware switch instantly triggers all inflation valves and powers the compressor to maximum capacity, rendering the mattress firm and rigid within seconds to enable chest compressions and emergency resuscitation.
* 🛡️ **Overpressure Relief:**  
  Mechanical pressure relief valves protect air chambers against over-inflation, safeguarding patient comfort and equipment longevity.

---

## 📅 5-Month Implementation Plan

| Month | Phase | Key Objectives & Deliverables |
| :---: | :--- | :--- |
| **Month 1** | **System Architecture & Hardware Planning** | System requirements specification, component procurement (microcontroller, valves, pump, sensors), pneumatic circuit and electronic schematic design. |
| **Month 2** | **Sensor Array Assembly & Calibration** | Fabrication of the pressure and temperature sensor matrix; calibration against body weight profiles; multi-channel ADC/multiplexer integration. |
| **Month 3** | **Pneumatic Actuation & Valve Circuitry** | Air pump driver circuit implementation; manifold and solenoid valve assembly; airtight bladder prototyping and power loss safety validation. |
| **Month 4** | **Firmware & Closed-Loop Control** | Embedded firmware development (ESP32/RTOS); adaptive pressure redistribution algorithm; CPR override logic; local fail-safe testing. |
| **Month 5** | **IoT Dashboard, Integration & Final Validation** | Real-time caregiver dashboard integration via MQTT; clinical stress testing; endurance and latency evaluation; project documentation and demonstration. |

---

## 🛠️ Technology Stack & Hardware Components

| Category | Components / Technologies |
| :--- | :--- |
| **Microcontroller / Compute** | ESP32-WROOM-32 / STM32 Embedded Platform |
| **Sensing Elements** | Force Sensitive Resistor (FSR) Array, DS18B20 / NTC Temperature Sensor Network, 16-channel Analog Multiplexers (CD74HC4067) |
| **Pneumatics & Actuation** | 12V DC Low-Noise Medical Air Pump, 12V 2-way/3-way Miniature Solenoid Valves, Relay/MOSFET Driver Modules, Multi-zone Polyurethane (TPU) Air Bladders |
| **Firmware & RTOS** | C/C++, FreeRTOS, Arduino / ESP-IDF Framework |
| **IoT & Telemetry** | MQTT Protocol, Eclipse Mosquitto, WebSockets, REST API |
| **Caregiver Dashboard** | React.js / Vite, TailwindCSS / Vanilla CSS, Chart.js / Heatmap.js |

---

## 👥 Team I.V.I.S

| eNumber | Name | Email |
| :---: | :--- | :---: |
| **E/22/330** | R. Shathursima | [e22330@eng.pdn.ac.lk](mailto:e22330@eng.pdn.ac.lk) |
| **E/22/373** | L. Sharmilan | [e22373@eng.pdn.ac.lk](mailto:e22373@eng.pdn.ac.lk) |
| **E/22/385** | S. Sulaxshan | [e22385@eng.pdn.ac.lk](mailto:e22385@eng.pdn.ac.lk) |
| **E/22/193** | S. Kishonithan | [e22193@eng.pdn.ac.lk](mailto:e22193@eng.pdn.ac.lk) |

---

## 🔗 Useful Links

* [Project Repository](https://github.com/cepdnaclk/e22_3YP_I.V.I.S)
* [Project GitHub Pages Site](https://cepdnaclk.github.io/e22_3YP_I.V.I.S)
* [Department of Computer Engineering](http://www.ce.pdn.ac.lk/)
* [Faculty of Engineering, University of Peradeniya](https://eng.pdn.ac.lk/)
