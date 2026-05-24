# CUBESAT_PowerDistribution_DHYAN_M
# CubeSat Electrical Power System (EPS)

A robust, high-reliability Electrical Power System (EPS) designed for a 1U/2U CubeSat architecture. This subsystem handles voltage regulation, dual-rail power distribution, and high-side power switching to ensure stable power delivery to the onboard computer (OBC) and mission payloads under varying battery conditions.

---

## Technical Specifications & Architecture

The EPS manages power distribution by stepping down raw battery voltage into stable DC rails and utilizes logic-level switching for autonomous payload isolation.

### 1. Power Regulation Architecture
* **Primary 5V Rail:** Handled by the **LM7805** linear voltage regulator, providing a dedicated, low-ripple power source for the central microcontroller/OBC (Arduino Nano platform).
* **Secondary 3.3V Rail:** Handled by the **LM1117-3.3** low-dropout (LDO) linear regulator, chained to provide low-noise power for onboard sensors, communication modules, and telemetry systems.

### 2. High-Side Power Switching & Telemetry
* **Power Switching:** Uses **IRF540N N-channel Power MOSFETs** configured for high-efficiency switching paths. This allows the microcontroller to dynamically cut or grant power to specific high-draw payloads to conserve battery.
* **Reverse Current & Spike Protection:** Integrated **1N5822 Schottky barrier diodes** guard the regulation stages against reverse-polarity transients, inductive spikes, and back-EMF from external sub-systems.

---

## System Block Diagram
[ Raw Battery Input ]
│
├──> [ 1N5822 Protection Diode ] ──> [ LM7805 (5V Regulator) ] ──> Stable 5V Rail ──> Arduino Nano (OBC)
│                                                                           │
│                                                                           └──> [ LM1117 (3.3V LDO) ] ──> Stable 3.3V Rail
│
└──> [ IRF540N MOSFET Switches ] ──> Dynamic Payload Isolation Channels (Controlled by OBC GPIO)

---

## Repository Structure

* `/CUBESAT_EPS.kicad_sch` - Main schematic file mapping out electrical connections and circuit design.
* `/CUBESAT_EPS.kicad_pcb` - Physical PCB layout file showing component footprints, track routing, and ground planes.
* `/CUBESAT_EPS.pdf` - High-resolution, production-ready schematic print for quick design reviews.
* `/CUBESAT_EPS.csv` - Bill of Materials (BOM) containing precise component values, quantities, and footprint configurations.
* `/Gerbers/` - Complete fabrication directory containing industry-standard Gerber files (`.gbr`) and Excellon drill files (`.drl`) compiled for PCB manufacturing.

---

## Tools & Technologies Used

* **KiCad EDA (v7/v8):** Used for complete Electronic Design Automation, including schematic capture, custom footprint verification, 2-layer PCB copper routing, zone fills (copper ground planes), and Design Rule Checking (DRC).
* **GitHub:** Utilized for hardware version control, managing design iterations, tracking development branches, and hosting open-source documentation.
* **Markdown:** Used to build clear, accessible engineering documentation for cross-functional team collaboration.

---

## Manufacturing & Assembly Notes

* **Layers:** 2-Layer Board (Top Copper `F.Cu` / Bottom Copper `B.Cu`).
* **Grounding:** Optimized with extensive cross-layer copper pours connected via stitching vias to minimize return path inductance and reduce electromagnetic interference (EMI).
* **Traces:** Power rails are routed with thickened traces to easily sustain maximum current limits without excessive thermal dissipation.
