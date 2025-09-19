# EzPowerV4 PCB Debugging and Simulation Guide

## Project Overview
- **Project**: EzPowerV4 EVSE Charging Station
- **Revision**: REV09
- **Date**: July 24, 2025
- **Description**: Comprehensive debugging guide for electronics simulation and PCB troubleshooting

---

## Electronics Simulation Software for 2025

### Free SPICE Simulators

#### **LTspice** (Analog Devices)
- **Best for**: Power electronics simulation
- **Features**:
  - Fast, powerful SPICE simulator
  - Extensive model library for power components
  - Excellent for switching regulator design
- **Download**: [analog.com/ltspice](https://www.analog.com/en/resources/design-tools-and-calculators/ltspice-simulator.html)
- **Use Case**: Simulate power supply chains (IRM-20-12, AP64200SP-13, AZ34063UMTR-G1)

#### **QSPICE** (Qorvo)
- **Best for**: Power electronics and RF applications
- **Features**:
  - Next-generation SPICE with improved performance
  - Specialized for power conversion circuits
  - Game-changing model generator for MOSFETs/diodes
- **Download**: [qorvo.com/qspice](https://www.qorvo.com/design-hub/design-tools/interactive/qspice)
- **Use Case**: Mixed-signal simulation of SPI interfaces and switching circuits

#### **KiCad + ngspice**
- **Best for**: Integrated PCB design and simulation
- **Features**:
  - Open-source integration
  - Seamless schematic-to-simulation workflow
  - Direct component model linking
- **Download**: [kicad.org](https://www.kicad.org/discover/spice/)
- **Use Case**: Verify EzPowerV4 schematic designs

#### **CircuitLab**
- **Best for**: Online collaboration and quick prototyping
- **Features**:
  - Browser-based SPICE simulation
  - Mixed analog/digital simulation
  - Cloud storage and sharing
- **URL**: [circuitlab.com](https://www.circuitlab.com/)
- **Use Case**: Quick verification of analog measurement chains

### Professional Power Electronics Tools

#### **PSIM**
- **Best for**: Power electronics and motor drives
- **Features**:
  - Specialized power conversion simulation
  - Thermal analysis capabilities
  - Embedded code generation
- **Use Case**: Simulate relay switching circuits (K1-K4) and power stage analysis

#### **PLECS** (Plexim)
- **Best for**: Power electronics with thermal simulation
- **Features**:
  - Switching and conduction loss calculation
  - Thermal modeling
  - Control system integration
- **Use Case**: Thermal analysis of 65A current paths

#### **PSpice** (Cadence)
- **Best for**: Industry-standard mixed-signal simulation
- **Features**:
  - 35,000+ parametrized models
  - Gold standard for analog/mixed-signal design
  - Advanced analysis capabilities
- **Use Case**: Complete system simulation with all components

#### **Multisim** (NI)
- **Best for**: Academic and research applications
- **Features**:
  - 55,000 component library
  - 30 simulated benchtop instruments
  - Integration with Ultiboard PCB layout
- **Use Case**: Educational analysis and comprehensive system verification

---

## EVSE-Specific Testing and Debugging Tools

### Professional Test Equipment

#### **Tektronix EVSE Testing Solutions**
- **Purpose**: Comprehensive EVSE validation
- **Capabilities**:
  - Communication protocol analysis (ISO/IEC 15118)
  - Power quality measurements
  - Safety compliance testing
- **URL**: [tek.com/evse-testing](https://www.tek.com/en/solutions/industry/automotive-test-solutions/evse-testing)

#### **Fluke FEV100 Adapter Kit**
- **Purpose**: EV charging station testing
- **Features**:
  - Simulates vehicle presence
  - Different resistance values for vehicle states
  - Compatible with DMMs and oscilloscopes
- **Use Case**: Test control pilot interface (U11 op-amp circuits)

#### **EVSE Simulator 2.0**
- **Purpose**: ISO/IEC 15118 communication testing
- **Features**:
  - PLC/HomePlug Green PHY simulation
  - DIN 70121 / SAE J2847/2 support
  - Complete charging protocol validation
- **URL**: [codico.com/evse-simulator](https://www.codico.com/en/charging-station-evse-simulator-2-0)

---

## Model Context Protocol (MCP) for Electronics Automation - 2025

### What is MCP?
Model Context Protocol is an open standard framework introduced by Anthropic for AI systems to integrate with external tools and data sources. In 2025, it has become a game-changer for electronics automation.

### Major Adoption in 2025
- **OpenAI**: Integrated MCP across ChatGPT and Agents SDK (March 2025)
- **Google DeepMind**: Confirmed MCP support in Gemini models (April 2025)
- **Microsoft**: Copilot Studio now supports MCP connections

### Electronics Design Automation MCP

#### **EDA MCP Server**
- **Purpose**: AI integration with electronics design tools
- **Capabilities**:
  - Verilog synthesis with Yosys
  - Circuit simulation with Icarus Verilog
  - ASIC flows with OpenLane
  - Visualization with GTKWave and KLayout
- **GitHub**: [github.com/modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers)

#### **Blender MCP**
- **Purpose**: 3D PCB visualization from text descriptions
- **Features**:
  - Convert 2D schematics to 3D scenes
  - AI-generated component placement
  - Interactive 3D debugging views
- **Use Case**: Visualize EzPowerV4 PCB layout issues

### Test Automation MCPs

#### **Browser MCP**
- **Purpose**: Automate web-based test equipment interfaces
- **Features**:
  - DOM-based element interaction
  - Structured accessibility snapshots
  - Reliable test automation
- **Use Case**: Automate oscilloscope and power analyzer controls

#### **Playwright MCP**
- **Purpose**: Enhanced browser automation
- **Features**:
  - Accessibility tree-based interaction
  - Form filling and navigation
  - Content extraction automation
- **Use Case**: Automated data collection from test equipment

---

## Common ATM90E32AS Issues in EzPowerV4

### Critical Communication Problems

#### **ESP32 Placement Issue**
- **Problem**: ESP32 placed "one row down too far" on PCB
- **Symptoms**: Complete communication failure with ATM90E32AS
- **Solution**: Verify U12 (ESP32-S3-WROOM-1U) correct pin alignment
- **Check**: Pins 36,37 (UART0) and SPI2 connections to U1 (STM32)

#### **SPI Pin Conflicts**
- **Problem**: Pin 19 (MISO) conflicts with other peripherals
- **Affected Signals**: `ATM90E_SPI1_MISO_ISO`
- **Check Points**:
  - U2 (ISO6742DWR) pin 13 to U5 (ATM90E32AS) pin 39
  - Verify isolation barrier integrity
  - Test SPI clock integrity on `ATM90E_SPI1_SCLK_ISO`

### Power Supply Validation Issues

#### **Isolated 3.3V Rail Problems**
- **Components**: U9 (PDSE1-S12-S3-S) → U10 (NXJ1S1205MC-R13) → U15 (TLV75533PDRVR)
- **Check Points**:
  1. **U9 Input**: +12V rail stability
  2. **U10 Isolation**: 1kV isolation barrier integrity
  3. **U15 Output**: +3.3V_ISO regulation
- **Common Issues**:
  - Inadequate input filtering (C56, C57)
  - Isolation transformer saturation
  - Load regulation problems

#### **Power Sequencing**
- **Critical**: Isolated domain must power up after main 3.3V rail
- **Monitor**: `+3.3V_ISO` vs `+3.3V` timing
- **Components**: U2 (ISO6742DWR) requires both domains stable

### Analog Frontend Problems

#### **Current Transformer Scaling**
- **Phase 1**: TR1 → R43-R49 (240kΩ each) → C29 (18nF) → U5 pins I1P:3, I1N:4
- **Phase 2**: TR2 → R56-R62 (240kΩ each) → C33 (18nF) → U5 pins I2P:5, I2N:6
- **Phase 3**: TR3 → R69-R75 (240kΩ each) → C37 (18nF) → U5 pins I3P:7, I3N:8

**Common Issues**:
- Incorrect voltage divider ratios for 65A scaling
- Filter capacitor ESR affecting frequency response
- CT saturation at high currents

#### **Voltage Measurement Scaling**
- **Phase 1**: R49,R52 → C30 → U5 pins V1P:13, V1N:14
- **Phase 2**: R64,R66 → C34 → U5 pins V2P:15, V2N:16
- **Phase 3**: R77,R79 → C38 → U5 pins V3P:17, V3N:18

**Validation**:
- 400V AC input should scale to ATM90E32AS range
- Verify 0.5% tolerance resistors (R50,R51,R54,R55, etc.)

### Ground Separation Issues

#### **AC/DC Ground Isolation**
- **Problem**: Confusion about AC and DC ground separation
- **Critical Points**:
  - `GND_3.3V_ISO` must be isolated from `GND`
  - Earth connection through M4 screws (MECH1, MECH2)
  - Isolation maintained across U2 (ISO6742DWR)

#### **Safety Ground**
- **Connection**: AC input EARTH → chassis ground via mechanical connection
- **Verification**: Continuity test between Earth pin and PCB ground plane

---

## Systematic Debugging Approach

### Phase 1: Power Validation

#### **Step 1: DC Rails Verification**
```
Tools: DMM, Oscilloscope
Sequence:
1. Measure +12V from U8 (IRM-20-12)
2. Verify +3.3V from U6 (AP64200SP-13)
3. Check -12V from U7 (AZ34063UMTR-G1)
4. Validate +3.3V_ISO from U9→U10→U15 chain
5. Confirm +5V_ISO from U10
```

#### **Step 2: LTspice Power Supply Simulation**
```
Simulate:
- AC/DC converter efficiency and ripple
- Buck regulator transient response
- Isolated converter regulation
- Power sequencing timing
```

### Phase 2: Digital Communication

#### **Step 1: SPI Interface Verification**
```
Tools: Logic Analyzer, Oscilloscope
Check Points:
- U1 pins 17,13,12,15 (SPI1 master)
- U2 pins 3,4,12,13 (isolation input)
- U2 pins 14,13,11,10 (isolation output)
- U5 pins 38,40,39,37 (SPI slave)
```

#### **Step 2: QSPICE Mixed-Signal Simulation**
```
Simulate:
- SPI timing through isolation barrier
- Signal integrity at 10MHz SPI clock
- Digital isolator propagation delays
```

### Phase 3: Analog Measurement Chain

#### **Step 1: CT Input Network Analysis**
```
Tools: Function Generator, Spectrum Analyzer
Test Points:
- TR1,TR2,TR3 secondary outputs
- Voltage divider midpoints
- Filter capacitor performance
- ATM90E32AS analog inputs
```

#### **Step 2: PSIM Analog Simulation**
```
Simulate:
- CT burden resistor calculations
- Voltage divider frequency response
- Filter capacitor phase shift
- ADC input impedance effects
```

### Phase 4: System Integration

#### **Step 1: Control Pilot Interface**
```
Tools: EVSE Simulator, Oscilloscope
Test Sequence:
1. PWM generation from U1 pin 30
2. U11 op-amp signal conditioning
3. CP_READ feedback to U1 pin 20
4. Vehicle state simulation
```

#### **Step 2: EVSE Protocol Validation**
```
Tools: Protocol Analyzer
Verify:
- ISO/IEC 15118 communication
- Control pilot state transitions
- Safety interlocks (GFCI)
- Relay sequencing
```

### Phase 5: MCP-Enabled Automation

#### **Step 1: EDA MCP Server Setup**
```bash
# Install EDA MCP Server
git clone https://github.com/modelcontextprotocol/servers
cd servers/eda
pip install -r requirements.txt

# Configure for EzPowerV4 project
```

#### **Step 2: Automated Verification Flow**
```
Use AI to:
1. Generate test vectors for SPI communication
2. Automate power sequence validation
3. Create regression test suites
4. Generate simulation reports
```

---

## Key Measurements and Test Points

### Critical Test Points
| Test Point | Signal | Expected Value | Notes |
|------------|--------|----------------|-------|
| TP5 | +3.3V | 3.3V ±5% | Main digital rail |
| TP6 | +12V | 12V ±5% | Primary power rail |
| TP7 | -12V | -12V ±5% | Analog negative rail |
| TP8 | +3.3V_ISO | 3.3V ±5% | Isolated digital rail |
| TP9 | +5V_ISO | 5V ±5% | Isolated power rail |
| TP2,TP3,TP4 | Phase measurements | Per CT scaling | Energy meter inputs |

### Critical Timing Measurements
| Parameter | Specification | Measurement Point |
|-----------|---------------|-------------------|
| SPI Clock | 10MHz max | U5 pin 38 (SCLK) |
| Reset timing | >1ms hold | U5 pin 41 (RESET) |
| Power sequence | ISO after main | TP5 → TP8 delay |
| Relay switching | <10ms | K1-K4 coil drive |

---

## Emergency Troubleshooting Checklist

### ❌ No Communication with ATM90E32AS
1. ✅ Verify ESP32 U12 correct placement
2. ✅ Check +3.3V_ISO rail (TP8)
3. ✅ Test SPI signals through isolation barrier U2
4. ✅ Confirm ATM90E32AS crystal Y3 oscillation
5. ✅ Validate reset timing on U5 pin 41

### ❌ Incorrect Power Measurements
1. ✅ Calibrate CT scaling resistors (240kΩ networks)
2. ✅ Verify filter capacitor values (18nF)
3. ✅ Check voltage divider ratios
4. ✅ Test ADC reference voltage
5. ✅ Validate ground isolation integrity

### ❌ Relay Control Issues
1. ✅ Check +12V_RELAY rail stability
2. ✅ Verify GPIO drive levels from U1
3. ✅ Test relay coil resistance (K1-K4)
4. ✅ Confirm flyback diode placement (D8-D11)
5. ✅ Validate switching timing

### ❌ Control Pilot Problems
1. ✅ Check PWM output from U1 pin 30
2. ✅ Verify U11 op-amp power rails (±12V)
3. ✅ Test CP_READ signal integrity
4. ✅ Validate pilot resistance values
5. ✅ Confirm GFCI interface operation

---

## Recommended Software Workflow

### Quick Start (Free Tools)
1. **LTspice**: Power supply analysis
2. **KiCad+ngspice**: Schematic verification
3. **CircuitLab**: Quick analog simulations
4. **EVSE Simulator**: Protocol testing

### Professional Workflow
1. **QSPICE**: Mixed-signal simulation
2. **PSIM**: Power electronics analysis
3. **Tektronix Tools**: Hardware validation
4. **EDA MCP**: AI-assisted debugging

### Future Integration (2025+)
1. **MCP Automation**: Streamlined test flows
2. **AI-Assisted Debugging**: Pattern recognition
3. **Cloud Simulation**: Collaborative debugging
4. **Digital Twin**: Real-time system modeling

---

## Additional Resources

### Documentation
- [ATM90E32AS Datasheet](http://ww1.microchip.com/downloads/en/devicedoc/Atmel-46003-SE-M90E32AS-Datasheet.pdf)
- [ISO6742DWR Isolation Amplifier](https://www.ti.com/product/ISO6742)
- [ESP32-S3-WROOM-1U Datasheet](https://www.espressif.com/sites/default/files/documentation/esp32-s3-wroom-1_wroom-1u_datasheet_en.pdf)

### Community Resources
- [OpenEnergyMonitor Community](https://community.openenergymonitor.org/)
- [CircuitSetup Energy Meter Issues](https://github.com/CircuitSetup/Expandable-6-Channel-ESP32-Energy-Meter/issues)
- [ESPHome ATM90E32 Component](https://esphome.io/components/sensor/atm90e32/)

### Test Equipment Suppliers
- **Tektronix**: Professional oscilloscopes and power analyzers
- **Fluke**: Portable test equipment and EVSE adapters
- **Keysight**: High-end measurement instruments
- **Rohde & Schwarz**: EMC and power quality testing

---

*Document Version: 1.0*
*Last Updated: September 18, 2025*
*Project: EzPowerV4 REV09*