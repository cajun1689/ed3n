# Tested & Recommended Software

ED3N Hydro boards speak plain **GPIO** and **I²C**, so they work with *any* automation stack that can toggle pins and poll sensors.  
That said, the project began with one goal in mind:

> **“A plug-and-play board that shows off everything Mycodo can do.”**

---

## Mycodo — flagship integration

[Mycodo](https://kizniche.github.io/Mycodo/) is an open-source environmental controller written for the Raspberry Pi.  
Kyle Gabriel (author) graciously helped ensure the ED3N pinout matches Mycodo’s dosing and sensor modules.

| Why Mycodo pairs perfectly | Details |
|---|---|
| **Native dosing** | Map each of the Hydro’s nine pump outputs to Mycodo’s “Doser” modules—set ml/min or ml/second directly. |
| **Sensor auto-detect** | Atlas EZO™ I²C addresses appear in the GUI; just choose pH, EC, etc., and Mycodo logs & graphs instantly. |
| **PID & scheduling** | Use built-in PID loops to maintain pH/EC, or create cron-style schedules for nutrient mixes. |
| **Dashboard & alerts** | Grafana dashboards out of the box; email/SMS/Telegram alerts when values drift. |

### Quick-start with Mycodo

1. Flash Raspberry Pi OS Lite.  
2. Run the one-line installer from the Mycodo docs.  
3. Add **Nine Doser outputs** (GPIO 6, 13, 26, 16, 12, 5, 25, 24, 23).  
4. Add **Sensor inputs** for each Atlas EZO address (default 0x61, 0x62, …).  
5. Calibrate pumps (Mycodo Doser->Calibrate) and you’re ready to automate.

---

## Other stacks we’ve tested

| Platform | Notes |
|----------|-------|
| **Node-RED** | Use the `rpi-gpio out` node for pumps and `i2c-bus` contrib nodes for I²C sensors. |
| **Home Assistant** | GPIO control via the **Raspberry Pi GPIO** integration; sensor data over MQTT or I²C proxy scripts. |
| **Standalone Python** | Any library combo (e.g., `RPi.GPIO` + `smbus2`); see `examples/` in the GitHub repo. |
| **Custom C / Rust** | Tested with `pigpio` C library and the `rppal` crate in Rust—rock-solid for industrial deployments. |

*(If you’ve validated another platform, open an Issue or PR and we’ll add it here.)*

---

## Calibration reminder

Whatever software you choose, always:

1. **Prime** each pump line.  
2. **Run** for a fixed time (e.g., 30 s).  
3. **Measure** the volume, repeat 3–5×, average, and store the ml/s rate.  
4. Re-calibrate after changing tubing, voltage, or fluid viscosity.

---

## Need help?

* **Software questions:** Mycodo Discord / GitHub Discussions  
* **Board questions:** [support@ed3n.io](mailto:support@ed3n.io)

Happy automating!