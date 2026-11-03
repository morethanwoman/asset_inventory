# Hybrid Renewable Power Plant — Complete Purdue Model Asset Inventory & Dashboard

This repository provides an interactive visualization and documentation framework mapping all operational, control, network, protection, and security assets of a utility-scale **Hybrid Renewable Energy Plant (Solar PV, Organic Photovoltaic [OPV], and Battery Energy Storage System [BESS])** across the ISA-95 / IEC 62443 Purdue Reference Model.

---

## 1. Complete Asset Inventory by Purdue Level

### Level 0: Physical Process Layer
* **Solar PV Array:** Monocrystalline/polycrystalline PV strings, DC combiner boxes, string fuses, surge protection devices (SPDs), tracker slewing drives, tilt/azimuth position sensors.
* **Organic Photovoltaic (OPV) Subfield:** Flexible/printed OPV modules, low-profile flexible junction boxes, local DC collection nodes, specialized spectral/irradiance sensors.
* **Battery Energy Storage System (BESS) Enclosures:** Lithium iron phosphate (LFP) battery racks, cell monitoring modules, liquid/air HVAC thermal management chillers, coolant distribution units, clean-agent/aerosol fire suppression systems, combustible gas detectors ($CO, H_2$), DC main contactors.
* **Power Conversion Systems (PCS):** Central & string solar inverters, bidirectional BESS inverters (grid-forming/grid-following), DC-DC converters.
* **Substation Primary HV/MV Assets:** Medium Voltage (MV) to High Voltage (HV) step-up power transformers, Gas-Insulated Switchgear (GIS) / Air-Insulated Switchgear (AIS) circuit breakers, disconnectors, current transformers (CTs), voltage transformers (VTs/PTs), surge arresters, auxiliary station service transformers (ASST).

### Level 1: Basic Control & Instrumentation Layer
* **Substation Control & Protection:**
  * Intelligent Electronic Devices (IEDs): Numerical distance protection relays, overcurrent relays, transformer differential protection IEDs, merging units, phasor measurement units (PMUs).
  * Bay Control Units (BCUs): Bay-level interlocking and circuit breaker control units.
* **Plant & Generation Control Hardware:**
  * **Redundant Power Plant Controllers (PPC):** Primary & Secondary (Hot-Standby) industrial RTUs/PLCs executing active/reactive power regulation, ramp-rate control, voltage/frequency droop profiles, and curtailment commands.
  * **Tracker Controllers (SCU):** Solar Tracker Unit controllers executing astronomical positioning, backtracking algorithms, and wind stow profiles for standard PV and flexible OPV fields.
  * **Battery Management System (BMS) Master/Rack Controllers:** Aggregating cell telemetry, computing State-of-Charge (SoC) / State-of-Health (SoH), managing thermal/electrical safety interlocks.
  * **Meteorological Control Unit (MCU) / Weather Data Concentrators:** Meteorological station RTUs interfacing with pyranometers, ambient/back-of-panel temperature sensors, sonic anemometers, and barometric pressure sensors.
* **Level 0-1 Access Network Infrastructure:**
  * Ruggedized DIN-rail Industrial Access Switches (e.g., Westermo WeOS, Siemens RUGGEDCOM, Fortinet FGR series) supporting IEC 61850 GOOSE/MMS, RSTP, and Parallel Redundancy Protocol (PRP).

### Level 2: Supervisory Control & Local HMI Layer
* **Supervisory & Control Stations:**
  * Local Maintenance Operator HMI Workstations (visualizations, local override controls, commissioning interfaces).
  * Area PLCs / Sub-plant RTUs coordinating functional islands (Solar PV island, OPV island, BESS island).
* **Level 2 Distribution Network:**
  * Industrial Managed Distribution Switches providing ring/star topology interconnecting Level 1 access switches to Level 3 core infrastructure, enforcing micro-VLAN segmentation (VLAN 10: SCADA, VLAN 20: Protection/GOOSE, VLAN 30: Metering, VLAN 40: CCTV).

### Level 3: Plant Operations & Industrial Control Center (ICC)
* **SCADA Supervisory Servers (Redundant Cluster):**
  * Primary SCADA Server and Secondary/Hot-Standby Backup SCADA Server for real-time plant control, alarm handling, and automated dispatch.
* **Operations & Engineering Servers:**
  * Time-Series Process Historian (long-term data archiving of inverter efficiency, BESS cycling logs, weather metrics).
  * Engineering Workstations (EWS) for PLC/PPC/IED firmware updates and asset configuration repositories.
  * IEEE 1588 PTP / NTP Grandmaster Clock Servers for microsecond-accurate time synchronization across protection relays and SCADA nodes.
* **Plant Cybersecurity Infrastructure:**
  * Next-Generation Industrial Firewalls (NGFWs): Fortinet FortiGate / FGR series with Deep Packet Inspection (DPI) for Modbus TCP, DNP3, IEC 60870-5-104, IEC 61850 MMS/GOOSE.
  * Industrial Intrusion Detection System (IDS/IPS) for OT anomaly detection and network traffic monitoring.
  * Centralized Log Collector & SIEM appliance.
  * Privileged Access Management (PAM) Gateway (e.g., WALLIX PAM4OT) for authenticated, recorded vendor remote access.
* **Level 3 Core Network Infrastructure:**
  * High-performance modular Core Industrial Switches with VRRP router redundancy, LACP link aggregation, and strict traffic prioritization.

### Level 3.5: Industrial DMZ (IDMZ)
* **Hardware Data Diodes / Unidirectional Gateways:** One-way data export to corporate IT/cloud without inbound attack vectors.
* **Reverse Proxy & Gateway Servers:** Terminating external API calls and inspecting incoming payloads.
* **Secure Jump Servers / Bastion Hosts:** Mandatory staging hosts for remote engineering maintenance.
* **Patch & Antivirus Staging Relays:** Staging firmware binaries and definition updates before OT deployment.

### Level 4: Enterprise, Business Logistics & External Interfaces
* **Corporate Systems:** Enterprise Resource Planning (ERP), CMMS, business intelligence dashboards.
* **TSO / DSO SCADA Gateways & Secure RTUs:** Dedicated gateways communicating with Transmission/Distribution System Operators via ICCP (IEC 60870-6 TASE.2), IEC 104, or DNP3 over IP via encrypted IPsec VPNs.
* **Energy Market Aggregator & Trading API Gateways:** Secure API endpoints linking the hybrid plant to Virtual Power Plant (VPP) aggregators, electricity market exchanges (e.g., EPEX SPOT, Nord Pool), and automated bidding platforms via mTLS (TLS 1.3).

---

## 2. Interactive Dashboard Features

The provided `index.html` file includes:
1. **Horizontal Asset Density Chart:** Visualizing operational asset concentration per Purdue level using Chart.js.
2. **Comprehensive Asset Inspector:** Clickable Purdue levels displaying the complete breakdown of physical devices, controllers, network equipment, cybersecurity appliances, protocols, and IEC 62443 controls.
3. **Redundancy & Security Status Badges:** Visual indicators highlighting SCADA failover, PPC redundancy, PAM implementation, and Data Diode isolation.

---

## 3. How to Run

No build step or local web server installation is required.
1. Download `index.html`.
2. Double-click or open `index.html` in any web browser (Chrome, Firefox, Edge, Safari).