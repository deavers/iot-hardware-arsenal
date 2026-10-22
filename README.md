# 📡 IoT, Embedded Linux Firmware & Hardware Security Arsenal

![Platforms](https://img.shields.io/badge/Hardware-ESP32--S3%20%7C%20Arduino%20%7C%20ARM%2FMIPS-a6e3a1?style=flat-square&logo=espressif)
![Protocols](https://img.shields.io/badge/Protocols-UART%20%7C%20SPI%20%7C%20BLE%20GATT%20%7C%20nRF24-89b4fa?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

A hands-on hardware and embedded security repository exploring the full stack of smart devices — from extracting and reverse-engineering **ARM/MIPS Linux router firmwares** to auditing **UART/SPI hardware buses**, **Bluetooth Low Energy (`BLE GATT`)**, and **2.4 GHz `nRF24` wireless protocols** using **ESP32-S3** and **Arduino**.

---

## 📂 Repository Structure

```text
iot-hardware-arsenal/
├── 01-firmware-unpacker-and-scanner/  # Automated SquashFS extractor, block entropy plotter & ELF vulnerability scanner
├── 02-hardware-uart-spi-dumper/       # Pinout playbooks, U-Boot shell hijacking & ESP32 SPI NOR Flash dumper
├── 03-esp32-ble-gatt-security/        # BLE GATT service enumerator, telemetry stream analyzer & auth tester
└── 04-nrf24-rf-crypto-testbed/        # 2.4GHz packet sniffer, replay attack PoC & HMAC-SHA256 rolling-code defense
```

---

## 🗺️ RPG Skill Tree: From Firmware Tinkerer to Silicon Glitcher

### 🟢 Tier 1 (Lv. 1–25): Firmware Surgeon & Embedded Linux Analyst

- **📖 Books & Chapters:**
  - **Aditya Gupta** — *The IoT Hacker's Handbook: A Practical Guide to Hacking the Internet of Things (Apress)*
    - **Ch. 1 & 2:** IoT Threat Modelling & Attack Surface.
    - **Ch. 3 & 4:** Firmware Extraction & Reverse Engineering (Bootloaders, kernel images, `SquashFS`, `JFFS2`, `CramFS`, `binwalk`, `sasquatch`, `QEMU` user-mode & system emulation).
- **⚔️ Practical Training:**
  - Download real router/IP-camera firmware images, inspect their entropy profile with `binwalk -E`, unpack the `SquashFS` root filesystem, and emulate ARM/MIPS CGI/web binaries using `qemu-arm-static` / `qemu-mipsel-static` + **Ghidra**.
- **🛠️ Boss Project (`/01-firmware-unpacker-and-scanner`):**
  - Build an automated **Firmware Security Triage CLI** in Python/C++ that unpacks firmware images, calculates sliding-window entropy to distinguish compressed vs. encrypted partitions, scans `/etc/shadow` and `.pem`/`.key` files, and flags dangerous C sinks (`system`, `popen`, `strcpy`, `sprintf`) in embedded ELF binaries.

---

### 🔵 Tier 2 (Lv. 26–50): Hardware Bus Breaker (`UART` / `SPI` / `I2C` / `JTAG`)

- **📖 Books & Chapters:**
  - **Aditya Gupta** — *The IoT Hacker's Handbook*
    - **Ch. 5 & 6:** Hardware Hacking 101, `UART`, `SPI`, `I2C`, and `JTAG` Exploitation.
  - **Colin O'Flynn & Jasper van Woudenberg** — *The Hardware Hacking Handbook (No Starch Press)*
    - **Ch. 1–5:** Embedded System Architecture, Interfacing with Hardware, Reconnaissance, Serial Interfaces (`UART`/`SPI`/`I2C`) & Debug Interfaces (`JTAG`/`SWD`).
- **⚔️ Practical Training:**
  - Identify unpopulated `UART` header pads (`GND`, `TX`, `RX`, `VCC`) on a physical router/IoT PCB using a multimeter/logic analyzer, interrupt the `U-Boot` bootloader over serial (`115200 8N1`), append `init=/bin/sh` to kernel boot arguments, and obtain a physical root shell.
- **🛠️ Boss Project (`/02-hardware-uart-spi-dumper`):**
  - Build custom **ESP32-S3 / Arduino Firmware** that acts as a multi-protocol `UART` Bridge & `SPI Flash Reader` to dump 8-pin SOIC SPI NOR Flash chips (`W25Qxx`) directly to a PC for offline analysis.

---

### 🟣 Tier 3 (Lv. 51–80): Wireless & Radio Frequency Hunter (`BLE GATT` & `2.4 GHz`)

- **📖 Books & Chapters:**
  - **Aditya Gupta** — *The IoT Hacker's Handbook*
    - **Ch. 9:** Exploiting Bluetooth Low Energy (`BLE`) (GAP/GATT architecture, UUIDs, characteristics, sniffing, MITM & replay).
    - **Ch. 10:** Exploiting Zigbee, Sub-GHz, and 2.4 GHz RF Protocols.
- **⚔️ Practical Training:**
  - Audit real-time `BLE GATT` heart-rate/sensor notification streams (building upon Amazfit Band 7 GATT integration) and test characteristic write permissions without pairing/bonding.
- **🛠️ Boss Project (`/03-esp32-ble-gatt-security` & `/04-nrf24-rf-crypto-testbed`):**
  - **Project A (`esp32-ble-auditor`):** Python + ESP32-S3 toolset that enumerates all BLE services/characteristics of nearby smart devices, logs notification payloads, and tests unauthorized GATT writes.
  - **Project B (`nrf24-rolling-code`):** Two-node `ESP32-S3 + nRF24L01` testbed demonstrating how raw unencrypted 2.4 GHz IoT commands are vulnerable to Replay Attacks, followed by a hardened implementation using monotonic counters and `HMAC-SHA256` authentication.

---

### 🔴 Tier 4 (Lv. 81–99): Silicon Sovereign (Side-Channel Analysis & Fault Injection)

- **📖 Books & Chapters:**
  - **Colin O'Flynn & Jasper van Woudenberg** — *The Hardware Hacking Handbook*
    - **Ch. 6 & 7:** Side-Channel Attacks, Simple Power Analysis (`SPA`) & Differential Power Analysis (`DPA`).
    - **Ch. 8–10:** Voltage Glitching, Clock Glitching & Electromagnetic Fault Injection (`EMFI`).
- **🛠️ Boss Project:**
  - Build a microcontroller **Voltage Glitching Testbed** (using an `ESP32-S3` + high-speed MOSFET crowbar circuit) to inject a sub-microsecond power drop into a target MCU during bootloader signature/password verification, bypassing Read-Out Protection (`RDP`).

---

## 🗺️ Mastery Progression Checklist

- [ ] **Lv. 1–25 (Firmware Unpacker):** *IoT Hacker's Handbook (Ch. 1–4)* — Firmware extraction, `binwalk`, ARM/MIPS ELF analysis in Ghidra.
- [ ] **Lv. 26–50 (Hardware Surgeon):** *IoT Hacker's Handbook (Ch. 5–7)* & *Hardware Hacking Handbook (Ch. 1–5)* — UART/SPI/JTAG debugging & U-Boot shell access.
- [ ] **Lv. 51–80 (RF & BLE Hunter):** *IoT Hacker's Handbook (Ch. 9–10)* — BLE GATT security auditing & 2.4 GHz `nRF24` rolling-code cryptography.
- [ ] **Lv. 81–99 (Silicon Sovereign):** *Hardware Hacking Handbook (Ch. 6–10)* — Side-Channel Power Analysis & Voltage Glitching.

---

## License

This project is licensed under the [MIT License](LICENSE).
