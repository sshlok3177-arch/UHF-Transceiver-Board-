# Design and Simulation of a UHF Communication Subsystem for a 3U CubeSat Mission

*Alternate title options (pick one):*
- *"Integrated Design of a UHF Transceiver Board with a Deployable Quadrifilar Helix Antenna for a 3U CubeSat"*
- *"A Low-Power UHF Communication Subsystem for a 3U CubeSat in LEO: System-Level Design and Simulation"*

**Authors:** Shlok Sharma, Hiten Dhiman, Vedant Vaidya, Aalok Prajapati
**Affiliation:** MIT World Peace University (MIT-WPU), Pune, India
**Corresponding author email:** sterg@mitwpu.edu.in
**Target venue:** IEEE-format conference paper (academic submission)

---

## Abstract
[150–250 words. Write last. Will cover: problem (UHF TT&C for a 3U CubeSat in 500 km LEO whose payload performs onboard edge-intelligence image processing, so the comm link only needs to return processed results rather than raw imagery — motivating a low-rate, low-power, high-reliability design); approach (integrated subsystem — Si4464 transceiver with Mini-Circuits PMA-7+ external PA, STM32U575 MCU under FreeRTOS, CCSDS + Reed-Solomon stack, deployable 4-turn LHCP quadrifilar helix antenna with spring + burn-wire release, L-network matching, Chebyshev LPF and BPF); key simulated numbers (antenna S11 ≈ −25 to −30 dB, link margins at 10°/30°/90° elevation at 500 km); contribution (documented, self-consistent system-level design and simulation of a complete CubeSat UHF subsystem co-designed with an edge-AI payload).]

## Keywords
CubeSat, UHF communication, quadrifilar helix antenna, impedance matching, link budget, GFSK, CCSDS, FreeRTOS, Reed-Solomon, STM32

---

## 1. Introduction

### 1.1 Mission context
This work presents the UHF communication subsystem developed for a 3U CubeSat mission targeting a 500 km low Earth orbit. The spacecraft's payload captures visible (RGB) and ultraviolet imagery of the Earth and performs onboard image processing and inference — *edge intelligence in space* — so that the communication link carries compact processed data products, telemetry, and command traffic rather than raw image data. This mission architecture relaxes the required downlink data rate and shifts the subsystem design priorities toward **link reliability, low power, and deployment heritage**, which together motivate the choices presented in this paper.

The UHF band was chosen for its well-understood propagation, modest ground-station requirements, and suitability for low-rate, high-reliability TT&C links. The subsystem operates with a 401–402 MHz transmit band and a 402–403 MHz receive band, within the allocations used for space operations and space research.

### 1.2 Prior work
[TBD — 3–5 references. I can populate common ones: NASA CubeSat Handbook; Muri & McNair (2012) survey of CubeSat RF; AX.25 and CCSDS protocol references; QFH antenna papers (Kilgus 1969 is the original, Amin 2008 for CubeSat use); Si446x CubeSat implementations. User to confirm which to cite.]

### 1.3 Contribution
This paper presents the integrated system-level design and simulation of a UHF communication subsystem for a 3U CubeSat, covering the RF front-end, deployable antenna, matching network, firmware stack, and link budget. The contribution is not a single novel component but a documented, self-consistent subsystem design where antenna, matching, and link-layer parameters are jointly optimized against a 500 km LEO link budget for elevation angles of 10°, 30°, and 90°.

---

## 2. System Architecture

[FIGURE 1: Block diagram — MCU ↔ Transceiver ↔ Matching Network ↔ Filter ↔ Antenna, plus power rails and deployment driver. User to confirm; I can sketch it textually first.]

| Parameter | Value |
|---|---|
| TX frequency band | 401–402 MHz |
| RX frequency band | 402–403 MHz |
| Modulation | GFSK |
| Data rate | 9600 bps |
| MCU | STM32U575 (ARM Cortex-M33, ultra-low-power) |
| Transceiver | Silicon Labs Si4464 |
| Protocol stack | CCSDS |
| FEC | Reed-Solomon |
| RTOS | FreeRTOS |
| Board dimensions | 91 × 94 mm (PC/104-inspired custom form factor) |
| Nominal power | 2–3 W |
| Peak power | 5–6 W (worst case, TX with PA) |
| Supply rails | 3.3 V (digital / transceiver), 12 V (external PA) |
| External power amplifier | Mini-Circuits PMA-7+ (UHF-capable broadband E-PHEMT MMIC) |

The STM32U575 was selected for its ultra-low-power operating modes, enabling duty-cycled operation between passes; the Si4464 was chosen for its native GFSK support, integrated packet handling, and wide supply range suitable for CubeSat power constraints.

---

## 3. Antenna Design and Simulation

### 3.1 Topology
A deployable four-turn quadrifilar helix antenna (QHA/QFH) was designed to provide left-hand circular polarization (LHCP) with near-hemispherical coverage, which is well-matched to CubeSat tumbling and low-elevation communication scenarios.

### 3.2 Deployment
The antenna uses a combined **spring-release and burn-wire** deployment mechanism: a resistive burn-wire element retains the stowed antenna against a spring force; on command, current through the wire melts the retention, and the spring extends the helix elements to the deployed geometry. [User to confirm material choices, current level, burn time at a high level — without CAD specifics.]

### 3.3 Simulation setup
Electromagnetic simulation was performed in Ansys HFSS. [User to provide: boundary conditions used, solver type (driven modal / terminal), mesh refinement, any CubeSat chassis model included.]

### 3.4 Simulated results
- Return loss (S11): **−25 to −30 dB** at the operating band (best case).
- [FIGURE 2 — S11 plot vs. frequency. User to export from HFSS.]
- [FIGURE 3 — Radiation pattern, 3D or elevation/azimuth cuts. User to export.]
- Gain: [TBD]
- Axial ratio (for CP): [TBD — important for QFH papers, reviewers expect it]
- −10 dB impedance bandwidth: [TBD]
- Radiation efficiency: [TBD]

---

## 4. RF Front-End and Impedance Matching

### 4.1 Functional description
The RF chain between the Si4464 transceiver and the deployable QFH antenna includes an external power amplifier, lumped-element impedance matching, and two cascaded filter stages. The signal path (TX direction) is:

`Si4464 TX → matching → BPF → PMA-7+ PA → LPF → antenna`

### 4.2 Matching network
The matching network uses a lumped **LC L-network** topology. An L-network was selected over Pi or T topologies for its minimal component count (two reactive elements), low insertion loss, and sufficient Q for the 1 MHz operational band centered around 401.5 MHz. Exact component values are not disclosed in this paper.

### 4.3 Filter design
Two Chebyshev filters are used:
- A **band-pass filter (BPF)** centered in 401–403 MHz for out-of-band rejection on the TX path ahead of the PA and on the RX path.
- A **low-pass filter (LPF)** after the PA for harmonic suppression (2f₀, 3f₀ attenuation).

Both filters were synthesized using **Ansys Nuhertz FilterSolutions** with a Chebyshev response chosen to maximize in-band passband flatness given the narrow operating band and to meet harmonic rejection targets with minimum order. [User: add order of each filter, e.g., 5th-order LPF, 3rd-order BPF, and passband ripple spec.]

### 4.4 Power amplifier
The Mini-Circuits PMA-7+ was selected as the external power amplifier on the TX path. It is a broadband E-PHEMT MMIC covering the UHF range, biased from the 12 V rail. [User: insert datasheet values at 400 MHz — typical gain (dB), P1dB (dBm), saturated Pout (dBm), and DC current at operating bias. These numbers feed directly into the link budget.]

### 4.5 Simulated RF chain performance
- Antenna return loss (S11): **−25 to −30 dB** in-band (best case — see §3).
- Matching network + filter chain simulated insertion loss: [TBD — state in dB, e.g., "< X dB across 401–403 MHz." *Note: do not claim 0 dB; all passive chains have finite loss.*]
- Combined chain return loss at antenna port: [TBD]
- Second/third harmonic rejection provided by LPF: [TBD — important, reviewers expect this for CubeSat RF papers]
- [FIGURE 4 — Simulated S-parameters (S11, S21) of matching + filter cascade.]

---

## 5. Mechanical Structure and Deployment

### 5.1 Board form factor and stack position
The communication board is 91 × 94 mm, derived from but not identical to the PC/104 standard, customized for the mechanical constraints of the 3U CubeSat chassis. The communication board is placed at the **nadir end** of the 3U stack — i.e., the face pointing toward Earth in the mission's nominal attitude — so that the deployable QFH antenna extends away from the spacecraft toward Earth. This placement was chosen to maximize the usable ground-visibility cone of the LHCP antenna pattern and to keep the antenna away from the payload aperture on the opposite face. [User: board mass (g) — TBD.]

### 5.2 Deployment mechanism
The antenna deployment combines a compression spring with a burn-wire release, as described in §3.2. This combination was chosen for its heritage in CubeSat missions, low part count, and single-shot reliability: the spring provides the deployment energy, and the burn-wire provides a reliable, commandable release mechanism with a well-characterized activation current. [User: any FEA / thermal sims for the deployment mechanism? If not, say so.]

### 5.3 Structural analysis
[TBD — modal frequency, first-mode result, static load analysis if done. User: have you run FEA on the board or just on the antenna? If none, this section can be dropped or merged into future work.]

---

## 6. Firmware and Protocol

### 6.1 Architecture
Firmware runs on FreeRTOS on the STM32U575. The architecture follows a layered model:
- **PHY:** Si4464 driver (SPI), packet assembly, GFSK configuration.
- **Data-link:** CCSDS framing with Reed-Solomon FEC.
- **Application:** TT&C handlers, command dispatcher, housekeeping telemetry.

[FIGURE 5 — Firmware architecture / task diagram. Show FreeRTOS tasks: RX task, TX task, housekeeping, watchdog, etc.]

### 6.2 Protocol choices
CCSDS (Consultative Committee for Space Data Systems) framing was adopted for interoperability with standard ground station software and heritage compatibility with space missions. Reed-Solomon FEC [specify: RS(255,223) is the CCSDS standard — confirm this is what you used] provides burst-error correction suited to fade events during low-elevation passes.

---

## 7. Link Budget

Link budget was computed for a 500 km circular LEO at three elevation angles: **10°, 30°, and 90°**. Slant range, free-space path loss, and atmospheric losses were evaluated for each.

### 7.1 Assumptions
| Parameter | Value |
|---|---|
| Orbit altitude | 500 km circular LEO |
| Elevation angles analyzed | 10°, 30°, 90° |
| Uplink frequency | 402.5 MHz (band center) |
| Downlink frequency | 401.5 MHz (band center) |
| Data rate | 9600 bps |
| Modulation | GFSK |
| FEC | Reed-Solomon RS(255,223), CCSDS standard |
| Required Eb/N0 for GFSK (BER 10⁻⁵, uncoded) | ~10.6 dB |
| Coding gain (RS(255,223)) | ~3 dB |
| Satellite TX chain | Si4464 + PMA-7+ external PA (combined Pout TBD from datasheet) |
| Satellite antenna | 4-turn LHCP QFH, nadir-pointing |
| Satellite antenna gain (boresight / 10° off) | [TBD from HFSS pattern] |
| Ground station antenna gain | [TBD] |
| Ground station G/T | [TBD] |
| Polarization loss assumption | 3 dB (CP-to-linear worst case) |

### 7.2 Results — TX (downlink) link budget
[TABLE — user's photo did not come through. Please paste the numbers or re-attach image.]

### 7.3 Results — RX (uplink) link budget
[TABLE — TBD.]

### 7.4 Link margin summary
| Elevation | Uplink margin (dB) | Downlink margin (dB) |
|---|---|---|
| 10° | TBD | TBD |
| 30° | TBD | TBD |
| 90° | TBD | TBD |

---

## 8. Results and Validation Plan

*(Renamed from "Measurements" — since hardware is not yet built, this section frames simulation results and describes the planned measurement campaign.)*

### 8.1 Summary of simulated results
- Antenna S11: −25 to −30 dB (best case) in 401–403 MHz band.
- Matching network: simulated insertion loss [TBD], return loss [TBD].
- Link margin: [TBD — populate from link budget].

### 8.2 Planned hardware validation
Once the flight board is fabricated, planned measurements include:
1. Antenna S11 on a calibrated VNA in a ground-plane-representative environment.
2. Radiation pattern measurement in an anechoic chamber (if available) or open-field.
3. End-to-end RF test using the Si4464 in loopback against a ground station receiver.
4. Power consumption characterization in nominal and peak modes.
5. Deployment test of the spring + burn-wire mechanism.

This measurement campaign is deferred to future work.

---

## 9. Discussion

### 9.1 Design tradeoffs
[**User — write this yourself.** Two paragraphs. Examples to cover:
- **Rate vs. link margin:** 9600 bps GFSK was selected because the edge-intelligence payload downlinks processed inference results and compressed metadata rather than raw imagery, so the link is sized for reliability (margin at 10° elevation) rather than throughput.
- **Antenna choice:** QFH with LHCP was selected over a simpler quarter-wave monopole for near-hemispherical coverage with consistent CP gain, avoiding the pattern nulls and polarization mismatch penalties of a linear element on a tumbling spacecraft.
- **Nadir placement:** communication board placed at the Earth-facing end of the 3U to maximize ground-visibility cone and keep the deployable antenna clear of the payload optical path.
- **Band choice:** 401–403 MHz over amateur 435 MHz — regulatory / licensing considerations for a university science mission.
- **MCU choice:** STM32U575 — ultra-low-power Cortex-M33 enables aggressive duty-cycling between ground-station passes.
- **PA choice:** PMA-7+ as external PA — selected for broadband UHF coverage and availability, trading some DC-to-RF efficiency against integration simplicity.
- **Protocol choice:** CCSDS framing + RS(255,223) — heritage, ground-station interoperability, burst-error tolerance for low-elevation fades.]

### 9.2 Limitations
- No flight hardware yet; results are simulation-only.
- Antenna pattern is simulated without the full CubeSat chassis — actual pattern will differ.
- Link budget uses idealized atmospheric loss model.
- [Add more from your own experience.]

---

## 10. Conclusion and Future Work

[**User — write this yourself.** Keep it to ~150 words. Honest: we designed and simulated; next step is fabrication, measurement, and integration testing.]

---

## Acknowledgements

[Advisor name, lab name, any funding / institutional support. User to fill.]

## References

[TBD — IEEE format. I'll populate with standard CubeSat / QFH / Si446x / CCSDS references once the body is stable. ~20 references for a conference paper.]

---
---

# === WORKING NOTES (will delete before submission) ===

## Outstanding gaps — still need:
1. **TX link budget image never came through — paste numbers as text, or re-attach.**
2. **Ground station assumptions** — antenna gain (dBi), system noise temperature or G/T. Without these, link margin cannot be computed.
3. **PMA-7+ datasheet numbers at ~400 MHz** — typical gain (dB), P1dB (dBm), Psat (dBm), DC bias current. User to pull from Mini-Circuits datasheet.
4. **Filter orders** — LPF order, BPF order, passband ripple spec.
5. **Antenna additional sim numbers** — gain (dBi), axial ratio (critical for CP antenna papers), -10 dB bandwidth, radiation efficiency. User said files aren't on hand — will need to pull from HFSS later.
6. **Board mass** (grams) — TBD when BOM is finalized.
7. **FEA results** — board / antenna / structure. If none, Section 5.3 should be dropped or moved to future work.
8. **Launch timeline / mission partner** — optional, strengthens intro if available.
9. **Firmware validation status** — written and tested on hardware, or written but untested?
10. **Prior-art references** — will need ~5 concrete citations for §1.2. I can suggest defaults.

## Answered — fill-ins captured:
- ✅ Matching: L-network
- ✅ Filters: Chebyshev LPF + Chebyshev BPF (orders TBD)
- ✅ Supply: 3.3 V + 12 V (12 V for PA)
- ✅ External PA: Mini-Circuits PMA-7+
- ✅ FEC: CCSDS standard (RS(255,223))
- ✅ Payload mission: RGB + UV Earth imaging with onboard edge intelligence
- ✅ Board position: nadir end of 3U (Earth-facing, antenna points down)
- ✅ Firmware: written (FreeRTOS)

## IP discipline checklist (unchanged)
- [x] No schematics, only block diagrams
- [x] No BOM / exact part numbers except widely-used ICs (Si4464, STM32U575) that are impossible to hide and not secret
- [x] No matching network component values — topology class only
- [x] No firmware source, only architecture diagrams
- [x] No CAD files / exact geometry — normalized or functional descriptions
- [x] Simulation plots ARE fine to publish

## Review flags (fix before submission)
- [ ] "S21 = 0 dB meaning zero reflection" — WRONG. S21 is transmission, S11 is reflection. Rewrite as simulated insertion loss in dB.
- [ ] Replace all "ideal / theoretical 0 dB" claims with actual simulated values.
- [ ] Section 8 is simulation-only right now; be explicit about that in the abstract and intro so reviewers don't expect measurements.

## Sections Shlok writes himself (for voice)
- Section 1.3 contribution statement (I drafted; rewrite in your voice)
- Section 9 Discussion
- Section 10 Conclusion
- Figure captions
- All numeric values
