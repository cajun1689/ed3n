# Hydro Lite

A compact control board for automated hydroponic systems.  
It drives **eight 12 V nutrient-dosing pumps plus one 12 V master pump**, letting you pre-mix before filling the reservoir.  
No soldering is required—boards arrive fully assembled and electrically tested (sold on Amazon).

!!! tip "Quick links"
    * [Schematic PDF](../hardware/hydro-lite/hydro-lite-schematic.pdf)
    * [Buy pre-assembled on Amazon](https://amazon.com/your-listing) *(coming soon)*

---

## Features
| &nbsp; | &nbsp; |
|---|---|
| MCU | ATtiny1624 @ 16 MHz (Optiboot) |
| Pump outputs | 9 × N-MOSFET (8 nutrient, 1 master) @ 12 V / 5 A each |
| Supply | 9 – 15 V DC barrel jack |
| Sensor bus | 3-pin JST-PH I²C (3 .3 V logic) |

---

## Schematic

![Hydro Lite schematic](../images/hydro-lite/hydro-lite-schematic.png)

*(Click the image for the full-resolution PDF.)*

---

## Jumper Settings – I²C Pull-ups

!!! note "H1 / H2 pull-up jumpers"
    * **Purpose:** adds 4 .7 kΩ pull-ups to **SDA** and **SCL**.  
    * **Use when:**  
        * A sensor board *lacks* pull-ups, **or**  
        * Cable length > 1 m.  
    * Extra pull-ups sit **in parallel** with existing ones—safe for mixed devices.

| Jumper | Default | Closed |
|--------|---------|--------|
| **H1 (SDA)** | open | adds 4 .7 kΩ pull-up |
| **H2 (SCL)** | open | adds 4 .7 kΩ pull-up |

---

## Bill of Materials (BOM excerpt)

| Qty | Designators | Part | LCSC # |
|----:|-------------|------|--------|
| 8 | CN1–CN8 | BM04B-SRSS-TB | C160390 |
| 9 | D1–D9 | SS14 | C2837270 |
| 1 | DC1 | DC-005-5A-2.0 jack | C381116 |
| 1 | EXTRA_HEADER | PZ254V-12-10P | C492422 |
| 1 | F1 | FSMD200-16R fuse | C220154 |
| 4 | H1–H4 | 2-pin header | C492421 |
| 2 | J1–J2 | 3-pin JST-PH | C145956 |
| 1 | L1 | 10 µH inductor | C14877 |
| 2 | Q1–Q2 | AO4407A MOSFET | C10486 |
| 9 | R1–R9 | 10 kΩ 0603 | C25803 |
| 4 | R10–R13 | 4 .7 kΩ 0603 | C25804 |
| 2 | U1–U2 | AMS1117-3 .3 V regulator | C6186 |
| 1 | U3 | ATtiny1624-SS | C347880 |
| 2 | C1–C2 | 10 µF 0805 | C15850 |
| 6 | C3–C8 | 100 nF 0603 | C16346 |

*Download the full CSV:* [hardware/hydro-lite/bom.csv](../hardware/hydro-lite/bom.csv)

---

## Controlling the Pumps

Each MOSFET channel is wired to a dedicated Raspberry Pi GPIO pin.  
Set the pin **HIGH** to energise the MOSFET and run the pump; set it **LOW** to stop.

| Connector label | Pi GPIO |
|-----------------|---------|
| **Master Pump** | 6  |
| **Pump 1** | 13 |
| **Pump 2** | 26 |
| **Pump 3** | 16 |
| **Pump 4** | 12 |
| **Pump 5** | 5  |
| **Pump 6** | 25 |
| **Pump 7** | 24 |
| **Pump 8** | 23 |

### Calibration workflow

1. **Prime** each pump tubing with water or nutrient.  
2. In your control software (Python, Node-RED, etc.) turn one pump **on** for a known time — e.g. **30 seconds**.  
3. Measure the volume dispensed (graduated cylinder works well).  
4. Repeat **3–5 times** and average the results to spot any deviation.  
5. Enter that ml/sec (or ml/min) rate into your dosing algorithm.

> **Tip:** Re-calibrate whenever you change tubing length, pump voltage, or fluid viscosity.

---

## Assembly & Test

Boards purchased on Amazon are **pre-assembled and tested**.  
For DIY assembly:

1. Solder MCU, regulator, and passives.  
2. Apply 9 V; verify 3 .3 V rail.  
3. Flash Optiboot via the UPDI header.  
4. Run **blink-pump.py** to toggle each MOSFET and confirm outputs.

---

## Revision History

| Rev | Date | Notes |
|-----|------|-------|
| v1.0.0 | 2025-06-10 | First public release |
