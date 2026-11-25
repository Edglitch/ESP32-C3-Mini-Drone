# 🚁 ESP32-C3 DIY Mini Drone (Sub-₹1,500 / $18 Build)

An ultra-budget, open-source micro quadcopter built from scratch using the **ESP32-C3 (RISC-V)** microcontroller, an **MPU-6050 6-Axis IMU**, and **AO3400 MOSFET drivers**. 

Zero expensive radio transmitters required—the drone hosts its own local Wi-Fi Access Point and serves an interactive **dual touchscreen joystick web controller** with real-time WebSocket telemetry directly to your smartphone.

---

## 📸 Project Status
> ⚙️ **Current Phase:** Hardware schematic verified & firmware tested. Final physical assembly and maiden flight test in progress!

*(Photos and flight test GIF coming soon after physical assembly)*

---

## ✨ Key Features & Specifications

* **Microcontroller:** Espressif ESP32-C3 SuperMini (32-bit RISC-V @ 160MHz, Wi-Fi / BLE, ~1.5g)
* **Attitude Sensor:** GY-521 (MPU-6050 3-Axis Gyroscope + 3-Axis Accelerometer)
* **Flight Loop Rate:** 200Hz (every 5ms) deterministic PID stabilization loop
* **Propulsion:** 4x 820 Coreless Brushed DC Motors (8x20mm, ~45,000 RPM) + 55mm Propellers
* **Motor Drivers:** 4x AO3400 N-Channel Logic-Level MOSFETs (30V, 5.8A continuous)
* **Power Supply:** 1S 3.7V 600mAh 25C LiPo Battery (~15A continuous discharge)
* **Brownout Protection:** 220µF Low-ESR Rubycon buffer capacitor across battery rails
* **Controller Interface:** Zero-install mobile web app with independent multi-touch joysticks and Safety Arm/Disarm switch
* **Total Estimated Weight (AUW):** ~55g – 60g
* **Thrust-to-Weight Ratio:** ~2.6 : 1 (plenty of punch and authority)
* **Total Build Cost:** **< ₹1,500 INR (~$18 USD)**

---

## 💰 Bill of Materials (BOM) & Budget

| Component | Description / Specification | Qty | Approx Cost (INR) |
| :--- | :--- | :---: | :--- |
| **ESP32-C3 SuperMini** | RISC-V 160MHz MCU, Type-C, Onboard 3.3V LDO | 1 | ₹250 |
| **GY-521 (MPU-6050)** | 6-DOF IMU (I2C Bus) | 1 | ₹150 |
| **820 Coreless Motors** | 8.0 × 20mm Coreless Brushed Motors + 55mm Props | 4 | ₹385 |
| **AO3400 N-MOSFETs** | 30V 5.8A Logic-level Gate (SOT-23) | 4 | ₹12 |
| **SS14 Schottky Diodes**| 40V 1A High-speed Flyback Protection (SMA) | 4 | ₹16 |
| **10kΩ Resistors** | 1206 SMD (Gate Pulldown) | 4 | ₹2 |
| **Rubycon 220µF Cap** | 10V Ultra-Low ESR Buffer Capacitor | 1 | ₹6 |
| **1S 600mAh 25C LiPo** | 3.7V High-Discharge LiPo Battery | 1 | ₹349 |
| **TP4056 Charger** | 1S LiPo Type-C USB Charging Module | 1 | ₹25 |
| **DIY Frame & Wire** | Lightweight 3D printed / balsa frame + perfboard | 1 | ~₹50 |
| **TOTAL** | | | **Approx.₹1,245($14 USD)+Delivery Charges** |

---

## 🔌 Circuit Schematic & Pin Mapping

The full hardware schematic was designed in **KiCad 8**.

### Pin Connection Table:
| ESP32-C3 SuperMini Pin | Connected To | Function |
| :--- | :--- | :--- |
| **Pin 1 (5V / VIN)** | Battery (+) Rail via Connector | Feeds onboard 3.3V LDO regulator |
| **Pin 2 (GND)** | Battery (−) Rail & Common Ground | Shared reference ground |
| **Pin 3 (3V3)** | MPU-6050 VCC | Regulated 3.3V logic supply |
| **Pin 8 (GPIO 0)** | Motor 1 Gate (Front-Left, CW) | 500Hz PWM Channel |
| **Pin 7 (GPIO 1)** | Motor 2 Gate (Front-Right, CCW) | 500Hz PWM Channel |
| **Pin 6 (GPIO 2)** | Motor 3 Gate (Rear-Right, CW) | 500Hz PWM Channel |
| **Pin 5 (GPIO 3)** | Motor 4 Gate (Rear-Left, CCW) | 500Hz PWM Channel |
| **Pin 12 (GPIO 8)** | MPU-6050 SDA | I2C Data Line |
| **Pin 13 (GPIO 9)** | MPU-6050 SCL | I2C Clock Line |
| — | **MPU-6050 AD0 Pin** | Tied to GND (sets address to 0x68) |

---

## 🕹️ Smartphone Web Controller (Mode 2)

No app download is needed. When powered on, the ESP32 broadcasts a private Wi-Fi network:
1. Connect smartphone to Wi-Fi: **`ESP32-Mini-Drone`** (Password: `12345678`).
2. Open browser and navigate to: `http://192.168.4.1`.
3. Tap **"DISARMED"** to arm the drone.
4. **Left Stick:** Throttle (Altitude) & Yaw (Rotation).
5. **Right Stick:** Pitch (Forward/Backward) & Roll (Left/Right Bank).

---

## 🚀 How to Build & Flash Firmware

1. Install [Arduino IDE](https://www.arduino.cc/en/software).
2. Add ESP32 board package URL in Preferences:
   ```text
   https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
   ```
3. Install required libraries via Library Manager:
   * **`MPU6050_light`** by rfetick
   * **`WebSockets`** by Markus Sattler
4. Select Board: **`ESP32C3 Dev Module`**.
5. Set **`USB CDC On Boot`** to **`Enabled`** under the Tools menu.
6. Open `/Firmware/Drone_Flight_Controller.ino` and upload to your ESP32-C3!

---

## 📜 License
This project is open-source and released under the **MIT License**. Feel free to build, modify, and fly!
