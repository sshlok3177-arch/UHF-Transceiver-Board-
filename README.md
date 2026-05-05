# UHF Transceiver Board

## Overview
The UHF Transceiver Board is a 4-layer PCB designed for space applications, 
specifically for CubeSats. It is built around the Si4464 transceiver IC, 
which has strong space heritage, and is designed to operate in the UHF 
frequency band with military-grade components for reliability in harsh 
space environments.

## Key Features
- **Frequency:** 401–402 MHz (UHF Band)
- **Modulation:** GFSK (Gaussian Frequency Shift Keying)
- **Duplex:** Half Duplex
- **Transceiver IC:** Silicon Labs Si4464 (space heritage)
- **Microcontroller:** STM32U5
- **PCB Layers:** 4-Layer
- **RF Output Connector:** SMA
- **Onboard Power Regulation:** Yes
- **Component Grade:** Military Grade
- **Application:** CubeSat Communication System

## How It Works
1. **Input** — STM32U5 microcontroller sends data to the Si4464 
   transceiver via SPI
2. **Modulation** — Si4464 modulates the data using GFSK modulation
3. **Transmission** — Modulated signal is transmitted at 401–402 MHz 
   via the SMA connector
4. **Reception** — Board receives incoming UHF signals in half duplex mode
5. **Output** — Received data is passed to the UHF Antenna Deployment 
   Board for phase shifting and LHCP antenna feeding

## Board Specifications
| Parameter | Value |
|---|---|
| Frequency | 401–402 MHz |
| Modulation | GFSK |
| Duplex Mode | Half Duplex |
| PCB Layers | 4 |
| Transceiver IC | Si4464 |
| Microcontroller | STM32U5 |
| RF Connector | SMA |
| Component Grade | Military Grade |
| Application | CubeSat |

## Files
| File | Description |
|---|---|
| `*.SchDoc` | Schematic documents |
| `*.PcbDoc` | PCB layout document |
| `*.PCBDwf` | PCB fabrication file |
| `*.BomDoc` | Bill of Materials |
| `*.PrjPcb` | Altium project file |

## Tools Used
- Altium Designer
- STM32CubeIDE

## Why Si4464?
The Si4464 was chosen for its proven space heritage, low power consumption,
and reliable performance in the UHF band making it ideal for CubeSat 
communication systems where reliability is critical.

## Why Military Grade Components?
Space environments expose electronics to extreme temperatures, radiation,
and vacuum conditions. Military grade components ensure the board operates
reliably throughout the mission lifecycle.

## Related Boards
- [UHF Antenna Deployment Board](https://github.com/sshlok3177-arch/UHF-Antenna-Deployment-Board) 
  — Receives output from this board and feeds the LHCP antenna

## License
This project is licensed under the MIT License - see the 
[LICENSE](LICENSE) file for details.
