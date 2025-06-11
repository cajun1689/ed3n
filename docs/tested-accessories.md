# Tested Accessories

Need sensors or add-ons that are proven on ED3N boards?  
This page tracks what we’ve validated. (Software setup lives on the [Tested Software](tested-software.md) page.)

---

## Atlas Scientific — best-in-class sensors

Hydro exposes **10 Atlas-ready headers** (4-pin: **GND · 3 V3 · SDA · SCL**):

| Header group | Count | Typical modules | Carrier needed? |
|--------------|------:|-----------------|-----------------|
| Carrier EZO™ | 5 | pH, EC, ORP, DO, RTD | **Yes** |
| Bare “ENV” EZO™ | 5 | CO₂, O₂, Humidity, Pressure, RGB | **No** |

### 1 · Switch UART ➜ I²C

| Method | Steps |
|--------|-------|
| **Manual jumpers** | Bridge each board’s I²C pads → LED turns **blue** |
| **\$13 toggler** | <https://atlas-scientific.com/ezo-accessories/i2c-toggler/> |

*(Pad locations: see datasheets below.)*

### 2 · Assign unique addresses

Default address = **99 dec (0x63)**.  
From any serial prompt:

```text
I2C,<new_decimal>        // then reboot

---
#### Suggested address map & datasheets

| Sensor | Dec | Hex | Datasheet |
|--------|----:|-----|-----------|
| pH | 100 | 0x64 | [PDF](hardware/atlas/pH_EZO_Datasheet.pdf) |
| EC | 101 | 0x65 | [PDF](hardware/atlas/EC_EZO_Datasheet.pdf) |
| Dissolved O₂ | 102 | 0x66 | [PDF](hardware/atlas/DO_EZO_Datasheet.pdf) |
| ORP | 103 | 0x67 | [PDF](hardware/atlas/ORP_EZO_Datasheet.pdf) |
| RTD (Temp) | 104 | 0x68 | [PDF](hardware/atlas/EZO_RTD_Datasheet.pdf) |
| CO₂ (ENV P) | 105 | 0x69 | [PDF](hardware/atlas/EZO_CO2_Datasheet.pdf) |
| O₂ (ENV P) | 106 | 0x6A | [PDF](hardware/atlas/EZO_O2_P_datasheet.pdf) |
| O₂ (ENV S) | 107 | 0x6B | [PDF](hardware/atlas/EZO-O2-S-datasheet.pdf) |
| Humidity (ENV P) | 108 | 0x6C | [PDF](hardware/atlas/EZO-HUM-P-P-Datasheet.pdf) |
| Humidity (ENV S) | 109 | 0x6D | [PDF](hardware/atlas/EZO-HUM-P-S-Datasheet.pdf) |
| Pressure (ENV) | 110 | 0x6E | [PDF](hardware/atlas/EZO-PRS-Datasheet.pdf) |
| RGB (ENV P) | 111 | 0x6F | [PDF](hardware/atlas/EZO_RGB_P_Datasheet.pdf) |
| RGB (ENV S) | 112 | 0x70 | [PDF](hardware/atlas/EZO_RGB_S_Datasheet.pdf) |

> Keep a small spreadsheet so you never reuse an address.