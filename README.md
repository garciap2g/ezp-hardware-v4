# EzPower V4 Hardware

This repository contains the hardware design files for the EzPower V4 system, an EVSE (Electric Vehicle Supply Equipment) charging station.

## Repository Structure

```
ezp-hardware-v4/
├── electronics/
│   ├── main_pcb/
│   │   ├── altium/
│   │   │   ├── EzPowerV4 - REV09.PrjPcb
│   │   │   ├── Layout/
│   │   │   │   ├── EzPowerV4 - REV09.PcbDoc
│   │   │   │   ├── EzPowerV4 - REV09 - Painel x2.PcbDoc
│   │   │   │   ├── EzPowerV4 - REV09 - Painel x4.PcbDoc
│   │   │   │   └── EzPowerV4 - REV09.step
│   │   │   └── Schematics/
│   │   │       ├── ESP32 WI-FI Module.SchDoc
│   │   │       ├── EVSE Control and GFCI.SchDoc
│   │   │       ├── Hardware_Architecture.SchDoc
│   │   │       ├── Microcontroller.SchDoc
│   │   │       ├── PCI Express.SchDoc
│   │   │       ├── Power Meter.SchDoc
│   │   │       ├── Power Supply.SchDoc
│   │   │       └── __Previews/ (schematic previews)
│   │   ├── bom/ (Bill of Materials - empty)
│   │   ├── gerber/
│   │   │   ├── Gerber EzPowerV4 - REV09.zip
│   │   │   └── Gerber EzPowerV4 - REV09 - Painel x2.zip
│   │   └── schematic/
│   │       └── EzPowerV4 - REV09.pdf
│   ├── led_panel/ (empty - reserved for LED panel electronics)
│   └── rfid/ (empty - reserved for RFID module electronics)
├── cables/ (empty - reserved for cable documentation)
├── case/ (empty - reserved for enclosure design files)
├── manuals/ (empty - reserved for documentation)
└── README.md
```

### Directory Details

#### Electronics
- **`electronics/main_pcb/`** - Main PCB design and manufacturing files
  - **`altium/`** - Complete Altium Designer project (REV09)
    - **Project file**: Main project container
    - **Layout/**: PCB layouts including single board and panel configurations (2x and 4x)
    - **Schematics/**: Seven schematic modules covering all system functions
  - **`gerber/`** - Manufacturing-ready Gerber files for PCB fabrication
  - **`schematic/`** - PDF documentation for design review
  - **`bom/`** - Reserved for Bill of Materials (currently empty)

#### Planned Components (Empty Directories)
- **`electronics/led_panel/`** - Future LED panel electronics
- **`electronics/rfid/`** - Future RFID module electronics
- **`cables/`** - Cable specifications and documentation
- **`case/`** - Enclosure and mechanical design files
- **`manuals/`** - User and technical documentation

## Main PCB Features

Based on the schematic modules, the main PCB includes:
- **ESP32 Wi-Fi Module** - Wireless connectivity
- **EVSE Control and GFCI** - Safety and charging control
- **Microcontroller** - Main processing unit
- **PCI Express** - High-speed communication interface
- **Power Meter** - Energy measurement and monitoring
- **Power Supply** - System power management

## File Formats

- **Altium Designer** (.PrjPcb, .PcbDoc, .SchDoc) - Native design files
- **Gerber** (.zip) - Manufacturing files for PCB fabrication
- **PDF** - Human-readable schematic documentation
- **STEP** - 3D mechanical models

## Getting Started

1. Open the Altium Designer project file: `electronics/main_pcb/altium/EzPowerV4 - REV09.PrjPcb`
2. Review the schematic documentation: `electronics/main_pcb/schematic/EzPowerV4 - REV09.pdf`
3. Use Gerber files for PCB manufacturing: `electronics/main_pcb/gerber/`