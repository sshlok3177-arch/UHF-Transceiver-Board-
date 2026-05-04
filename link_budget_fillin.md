# Link Budget Fill-In Sheet
## Fill in every blank. Leave blank if unknown — don't guess.

---

## A. Satellite TX chain (Si4464 → antenna)

A1. Si4464 TX output power ______________ dBm
A2. PMA-7+ gain at ~400 MHz ______________ dB
A3. PMA-7+ P1dB at ~400 MHz ______________ dBm
A4. PMA-7+ Psat at ~400 MHz ______________ dBm
A5. Total TX power at PA output ______________ dBm
A6. LPF insertion loss (post-PA) ______________ dB
A7. BPF insertion loss (pre-PA) ______________ dB
A8. Matching network insertion loss ______________ dB
A9. Cable / trace / connector loss ______________ dB
A10. Net power at antenna port ______________ dBm

---

## B. Satellite antenna (QFH)

B1. Peak gain (boresight) ______________ dBi
B2. Gain at 10° off-boresight ______________ dBi
B3. Gain at 30° off-boresight ______________ dBi
B4. Gain at 60° off-boresight ______________ dBi
B5. Axial ratio (CP quality) ______________ dB
B6. Radiation efficiency ______________ %
B7. −10 dB impedance bandwidth ______________ MHz
B8. EIRP (boresight) ______________ dBm

---

## C. Ground station (RX for downlink)

C1. GS antenna type ______________
C2. GS antenna gain ______________ dBi
C3. GS antenna polarization ______________
C4. Polarization mismatch loss ______________ dB
C5. GS feeder / cable loss ______________ dB
C6. GS LNA noise figure ______________ dB
C7. GS system noise temperature (Ts) ______________ K
C8. GS G/T ______________ dB/K
C9. GS pointing loss ______________ dB

---

## D. Ground station (TX for uplink)

D1. GS transmitter power ______________ dBm
D2. GS TX feeder loss ______________ dB
D3. GS TX antenna gain ______________ dBi
D4. GS EIRP ______________ dBm

---

## E. Satellite RX (uplink receive)

E1. Satellite RX antenna gain ______________ dBi
E2. Satellite RX chain loss (matching + BPF + cable) ______________ dB
E3. Si4464 noise figure ______________ dB
E4. Si4464 RX sensitivity at 9600 bps GFSK ______________ dBm

---

## F. Channel / geometry

F1. Orbit altitude ______________ km
F2. Slant range at 90° elevation ______________ km
F3. Slant range at 30° elevation ______________ km
F4. Slant range at 10° elevation ______________ km
F5. FSPL at 90° elevation (401.5 MHz) ______________ dB
F6. FSPL at 30° elevation ______________ dB
F7. FSPL at 10° elevation ______________ dB
F8. Atmospheric absorption ______________ dB
F9. Ionospheric scintillation allowance ______________ dB
F10. Rain / weather margin ______________ dB
F11. Implementation loss ______________ dB

---

## G. Required performance

G1. Target BER ______________
G2. Required Eb/N0 for GFSK uncoded ______________ dB
G3. Coding gain (RS 255,223) ______________ dB
G4. Required Eb/N0 post-coding ______________ dB

---

## H. Link margin results

Downlink margin at 10° ______________ dB
Downlink margin at 30° ______________ dB
Downlink margin at 90° ______________ dB

Uplink margin at 10° ______________ dB
Uplink margin at 30° ______________ dB
Uplink margin at 90° ______________ dB

---

## I. Bonus / non-RF fields still outstanding

I1. Board mass ______________ g
I2. Firmware hardware-tested? (yes / no / partially) ______________
I3. Filter order — LPF ______________
I4. Filter order — BPF ______________
I5. Filter passband ripple ______________ dB
I6. Advisor / PI name for Acknowledgements ______________
I7. Any funding source to acknowledge ______________
I8. Launch / flight timeline (if known) ______________
