# UHF Transceiver Board

## Overview
The UHF Transceiver Board is a 4-layer PCB designed for space applications, 
specifically for CubeSats. It is built around the Si4464 transceiver IC, 
which has space heritage, and is designed to operate in the UHF 
frequency band with military-grade components for reliability in harsh 
space environments.

## Key Features
- **Frequency:** 401–402 MHz (UHF Band)
- **Modulation:** GFSK (Gaussian Frequency Shift Keying)
- **Duplex:** Half Duplex
- **Transceiver IC:** Silicon Labs Si4464 (space heritage)
- **Microcontroller:** STM32U575RGT6TR
- **PCB Layers:** 4-Layer
- **Application:** CubeSat Communication System

## Files
| File | Description |
|---|---|
| `*.SchDoc` | Schematic documents |
| `*.PcbDoc` | PCB layout document |
| `*.PCBDwf` | PCB fabrication file |
| `*.PrjPcb` | Altium project file |

## Tools Used
- Altium Designer
- STM32CubeIDE

## Related Boards
- [UHF Antenna Deployment Board](https://github.com/sshlok3177-arch/UHF-Antenna-Deployment-Board) 
  — Receives output from this board and feeds the LHCP antenna

## License
This project is licensed under the MIT License - see the 
[LICENSE](LICENSE) file for details.
