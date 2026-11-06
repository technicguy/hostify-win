# HospitalityOS — Windows Desktop App (Offline Hub)

[![Platform](https://img.shields.io/badge/platform-Windows%2010%20%7C%2011%20(x64)-blue.svg)](#system-requirements)
[![Release](https://img.shields.io/badge/release-v1.5.3-emerald.svg)](releases/WindowsApp-Setup-1.5.3.exe)
[![Architecture](https://img.shields.io/badge/engine-Flutter%203.41%20%7C%20Dart%203.11-cyan.svg)](#technical-architecture)
[![License](https://img.shields.io/badge/license-Proprietary%20%2F%20Commercial-amber.svg)](#licensing)

![HospitalityOS](hostify.png)

> **HospitalityOS Offline Hub** is a native Windows desktop workstation engineered for hotels, resorts, and multi-outlet restaurants. It acts as an **autonomous local server & POS terminal**, operating 100% offline without relying on active internet connectivity or an external Apache/MySQL stack.

---

## 📥 Download Latest Release

| File Name | Version | Architecture | SHA256 Checksum | Direct Link |
| :--- | :---: | :---: | :--- | :--- |
| **`WindowsApp-Setup-1.5.3.exe`** | `v1.5.3` | `x64` (64-bit) | `19FE9F26C036F6A6F416134B15ACCB1A1E081643596577D488B921463F790DE8` | [Download Installer (21.0 MB)](releases/WindowsApp-Setup-1.5.3.exe) |

---

## 🚀 What's New in v1.5.3

### 1. 🎙️ Kitchen Display System (KDS) Voice Announcements (Native Windows SAPI)
- **Zero Cloud Dependencies**: Leverages the native Windows Speech API (`SAPI.SpVoice`) via hardened PowerShell execution (`-EncodedCommand` UTF-16LE) so voice alerts function in complete air-gapped isolation.
- **Dynamic Order Announcer**:
  - Automatically speaks newly received orders the instant they hit the local SQLite database.
  - Three configurable speech modes:
    - **Detailed**: Table/Room + specific item quantities (e.g., *"New order for Table 5. 2 Chicken Burger, 1 Lemon Tea."*).
    - **Compact**: Summary announcement with total count (e.g., *"New order for Table 5. 3 items."*).
    - **Alert Only**: High-urgency alert chime & verbal alert (*"New order received."*).
- **Speed Rate Control**: Adjustable speech playback speed (`0.7x` to `1.4x`) configured directly in Settings.
- **Live KDS Quick Toggle**: Live voice notification icon button in the KDS AppBar next to the existing kitchen chime.

### 2. 📋 Unrestricted KDS Order Items Display
- Fully removed item truncation restrictions (`.take(2)` and `+ more items...`).
- Kitchen staff see every item, modifier, and quantity directly on the board cards across **Pending**, **Preparing**, and **Completed** columns without needing extra clicks.

### 3. 🔄 Real-Time Reactive State Provider
- Re-architected `OrdersNotifier` in Riverpod to pull live settings snapshots on every order detection tick, eliminating stale setting states during live shifts.

---

## 🏛️ Core Features & Capabilities

```
+-------------------------------------------------------------------------+
|                       HospitalityOS Desktop Hub                         |
+--------------------+---------------------+------------------------------+
| Local SQLite DB    | Embedded Shelf Http | WebRTC Local Intercom        |
| (sqflite_common)   | (Port 8090 & 8443)  | Low-latency 2-way Voice      |
+--------------------+---------------------+------------------------------+
| ESC/POS Spooler    | Two-Way Sync Engine | Windows Native TTS           |
| (80mm Thermal POS) | Online <-> Offline  | Kitchen Speech Synthesizer   |
+--------------------+---------------------+------------------------------+
```

### 1. Embedded Shelf Local Server (LAN Digital Menu)
- Runs an embedded HTTP/HTTPS microserver directly inside the Flutter Windows process (`:8090` / `:8443`).
- Guests and staff on the local Wi-Fi can scan table QR codes to access menus and place orders directly onto the Windows Hub without requiring internet access.

### 2. Autonomous Local SQLite Database
- Powered by `sqflite_common_ffi` and native `sqlite3.dll`.
- All bookings, tables, orders, bills, and inventory transactions write directly to disk with zero network latency.

### 3. Bidirectional Offline Sync Engine (v2.0)
- Detects cloud availability in the background.
- When an internet uplink is detected, changes sync seamlessly with the live web system (`esanshar.com.np`) using transactional timestamp reconciliations.

### 4. Enterprise HRIS & Payroll Suite
- Employee attendance check-in/check-out.
- Monthly advance amortization & loan management.
- Batch payroll calculation with Nepalese tax & PAN compliance.

### 5. Hardware Peripherals Integration
- Direct print spooling for standard **80mm ESC/POS Thermal Receipt Printers**.
- Support for auto-printing KOTs (Kitchen Order Tickets) upon order placement.
- Support for cash drawer kick triggers via ESC/POS pulse codes.

---

## 💻 System Requirements

| Specification | Minimum | Recommended |
| :--- | :--- | :--- |
| **Operating System** | Windows 10 (64-bit, 1809+) | Windows 11 (64-bit) |
| **Processor** | Intel Core i3 / AMD Ryzen 3 (2.0 GHz) | Intel Core i5 / AMD Ryzen 5 or higher |
| **Memory (RAM)** | 4 GB | 8 GB or higher |
| **Storage** | 500 MB free storage | SSD with 1 GB+ free storage |
| **Display Resolution**| 1366 x 768 | 1920 x 1080 (Full HD) |
| **Network** | Local Wi-Fi / Ethernet router | Gigabit LAN router for multi-device ordering |

---

## 🛠️ Installation Guide

1. Download [`WindowsApp-Setup-1.5.3.exe`](releases/WindowsApp-Setup-1.5.3.exe).
2. Right-click the installer and choose **Run as administrator** (required to register local firewall rules for port 8090/8443 and configure program directories).
3. Follow the setup wizard to complete the installation.
4. Launch **HospitalityOS** from your Desktop shortcut or the Start Menu.
5. On the first launch:
   - Configure your **Offline Base URL** or connect to your local LAN router.
   - Set up your hotel/restaurant name, currency symbol, and peripheral printer preferences in **Settings**.

---

## 📂 Repository Structure

```
hostify-win/
├── releases/
│   └── WindowsApp-Setup-1.5.3.exe   # Compiled standalone installer (21.0 MB)
├── hostify.png                      # Application branding graphic
├── .gitignore                       # Git ignore definitions
└── README.md                        # Complete project documentation
```

---

## 🔒 Technical Architecture

- **UI Framework**: Flutter Desktop (Windows C++ Runner)
- **State Management**: Flutter Riverpod (`StateNotifierProvider`)
- **Typography & Design**: Google Fonts Outfit & Inter with Material Design 3
- **Local Audio**: `audioplayers` for local WAV/MP3 chime alerts
- **Speech Engine**: Windows SAPI (`System.Speech` / `SAPI.SpVoice`)
- **Local Server**: Dart Shelf framework (`shelf`, `shelf_router`, `http_multi_server`)
- **Networking**: `dio`, `web_socket_channel`, WebRTC P2P mesh
- **Packaging**: NSIS (Nullsoft Scriptable Install System) v3.x with solid LZMA compression

---

## 📞 Support & Inquiries

Developed and maintained by **Sanshar / Technicguy**.  
For licensing, multi-branch enterprise deployments, or custom hardware integrations:
- **Website**: [esanshar.com.np](https://www.esanshar.com.np)
- **Repository**: [github.com/technicguy/hostify-win](https://github.com/technicguy/hostify-win)
