# HospitalityOS — Windows Desktop App (Offline Hub)

[![Platform](https://img.shields.io/badge/Platform-Windows%2010%20%7C%2011%20(x64)-blue.svg)](#system-requirements)
[![Release](https://img.shields.io/badge/Release-v1.5.3-emerald.svg)](releases/WindowsApp-Setup-1.5.3.exe)
[![Architecture](https://img.shields.io/badge/Engine-Flutter%203.41%20%7C%20Dart%203.11-cyan.svg)](#technical-architecture)
[![License](https://img.shields.io/badge/License-Proprietary%20%2F%20Commercial-amber.svg)](#licensing--authorization)

![HospitalityOS](hostify.png)

> **HospitalityOS Offline Hub** is the dedicated enterprise Windows desktop companion for hotels, resorts, banquets, and multi-outlet restaurants. Engineered with an offline-first architecture, it provides an autonomous edge workstation that handles local order processing, kitchen display coordination, Wi-Fi intercom calling, and thermal receipt printing — even during prolonged internet outages.

---

## ⚠️ MANDATORY DEPENDENCY NOTICE

> [!CAUTION]
> ### 🛑 This Desktop App CANNOT Run Standalone Without the Hospitality Web System
> 
> **HospitalityOS Desktop is NOT an independent, isolated application.**  
> It is an **offline edge node / companion hub** specifically designed to link directly with your **Hospitality Management Web Platform** (e.g., hosted on `https://www.esanshar.com.np` or your private dedicated domain).
>
> 1. **Initial Provisioning & Sync**: On initial setup, you **MUST** provide your **Project Base URL** and authenticate using an authorized staff/admin account registered on your web system.
> 2. **Master Data Authority**: Menu items, room inventories, table maps, staff credentials, tax rates, and hotel business configurations originate from and belong to the web platform.
> 3. **Hardware Authorization & Node Licensing**: The app validates its node fingerprint and security access policy against the mother web system. Unregistered or unauthorized desktop instances will be locked.
> 4. **Bidirectional Ledger Synchronization**: All local bookings, offline POS bills, table changes, and KDS updates must sync back to the cloud ledger whenever connection is available.

---

## 📥 Download Official Release

| Release File | Version | Architecture | SHA256 Checksum | Download |
| :--- | :---: | :---: | :--- | :--- |
| **`WindowsApp-Setup-1.5.3.exe`** | `v1.5.3` | `x64` (64-bit) | `19FE9F26C036F6A6F416134B15ACCB1A1E081643596577D488B921463F790DE8` | [⬇️ Download Installer (21.0 MB)](releases/WindowsApp-Setup-1.5.3.exe) |

---

## 🌟 What's New in Version 1.5.3

* **Kitchen Display System (KDS) Native Voice Announcements**:
  * Employs native Windows Speech API (`SAPI.SpVoice`) via hardened PowerShell UTF-16LE `-EncodedCommand` execution.
  * Real-time text-to-speech announces incoming orders even without internet access.
  * Three selectable voice announcement profiles: **Detailed**, **Compact**, and **Alert Only**.
  * Speech rate slider (`0.7x` to `1.4x`) and live AppBar quick-toggle.
* **Full Order Item Visibility on KDS Cards**:
  * Completely eliminated the `.take(2)` limit and `+ more items...` truncation.
  * Every item, quantity multiplier (`1x`, `2x`), and preparation modifier is now visible across Pending, Preparing, and Completed board lanes.
* **Reactive Provider State Architecture**:
  * Replaced static initial settings with dynamic live Riverpod state reads on every background poll cycle.

---

## 📑 Comprehensive Feature Breakdown, Usage & Business Benefits

```
+----------------------------------------------------------------------------------------------------+
|                                    HospitalityOS Ecosystem                                        |
+--------------------------------------------------+-------------------------------------------------+
|              CLOUD WEB SYSTEM                    |              OFFLINE DESKTOP HUB                |
|           (esanshar.com.np)                      |                (Windows App)                    |
|                                                  |                                                 |
|  * Master Menu Catalog & Price Rules             |  * Embedded Shelf Web Server (:8090 / :8443)    |
|  * Room Categories & Reservation Booking Engine  |  * Autonomous SQLite Edge Database              |
|  * Multi-branch Ledger & Centralized Accounting  |  * Zero-Latency POS Billing & Receipt Printing  |
|  * HRIS, Attendance & Enterprise Payroll Engine  |  * Native Windows SAPI Kitchen Voice Alerts     |
|  * Node License & Machine Access Provisioning    |  * Local WebRTC & Wi-Fi Audio Staff Intercom    |
+--------------------------------------------------+-------------------------------------------------+
                                      \                       /
                                       \                     /
                                        ▼                   ▼
                               [ Bidirectional Sync Engine v2.0 ]
                                 (Automated Background Sync)
```

---

### 1. 🍽️ Kitchen Display System (KDS) & Native Voice TTS

#### How It Works:
Replaces paper tickets in the kitchen with a real-time digital display organized into three workflow columns: **Pending**, **Preparing**, and **Completed**. When an order is placed from a guest QR menu, POS terminal, or hotel room service, it enters the board instantly. Version 1.5.3 introduces a voice announcer powered by Windows SAPI that vocalizes orders through kitchen loudspeakers.

#### How to Use:
1. Open **Restaurant Management -> Active Orders (KDS)**.
2. In the top AppBar, click the **Voice Announce Icon** to switch TTS ON (blue) or OFF (grey).
3. Open **Settings -> Kitchen Voice Announcement (TTS)** to select your preferred announcement format:
   - **Full Detail**: *"New order for Table 5. 2 Chicken Burger, 1 Lemon Tea."*
   - **Compact**: *"New order for Table 5. 3 items."*
   - **Alert Only**: *"New order received."*
4. Adjust the **Speech Speed** slider (`0.7x`–`1.4x`) and click **Test Voice Announcement** to verify speaker volume.
5. Kitchen chefs click **Start Preparing** to advance an order, then **Mark Complete** when finished.

#### Business Benefits:
* **Zero Missed Orders**: Kitchen staff hear the exact table and items even when working away from the screen.
* **Faster Prep Times**: Eliminates hand-written tickets, kitchen runners, and illegible order handwriting.
* **100% Offline Resilience**: Windows SAPI synthesizes voice locally on your CPU without consuming bandwidth or requiring cloud API keys.

---

### 2. ⚡ Autonomous Local Server & Guest Digital QR Ordering

#### How It Works:
The Windows desktop app runs an embedded Dart Shelf microserver on port `8090` (HTTP) and `8443` (HTTPS). This transforms your desktop workstation into an in-house web server.

#### How to Use:
1. Connect your Windows PC and staff/guest devices to the same local Wi-Fi router.
2. The app automatically detects its local IP (e.g., `http://192.168.1.50:8090`).
3. Print table QR codes containing table-specific URLs directly from the app.
4. Guests scan the QR code with any smartphone camera to browse the menu, filter dietary options, and submit food/drink orders directly into the desktop app.

#### Business Benefits:
* **Works Without Internet**: Guests can view menus and submit orders even if your ISP connection goes down.
* **Reduced Staff Workload**: Guests self-order from their tables, freeing waitstaff to focus on service delivery.
* **Microsecond Response**: Submissions register in milliseconds over local Wi-Fi.

---

### 3. 💾 Autonomous SQLite Edge Database (`sqflite_common_ffi`)

#### How It Works:
All transactions, bookings, room statuses, orders, and customer profiles are stored locally on your SSD using native C++ `sqlite3.dll`.

#### How to Use:
* Database operations are completely automated in the background.
* Open **Settings -> Diagnostics -> Database Inspector** to view raw table rows, sync queue records, and cache health.

#### Business Benefits:
* **Crash-Proof Reliability**: ACID-compliant transactions protect your financial records against abrupt power failures.
* **Instantaneous UI Loading**: Tables, bills, and guest directories render with zero network loading spinners.

---

### 4. 🔄 Bidirectional Two-Way Offline Sync Engine (v2.0)

#### How It Works:
The background sync coordinator bridges your local desktop edge database with your master cloud system (`esanshar.com.np`).

```
[ Local Desktop Action ] ──► [ Local SQLite Save (last_sync_online = NULL) ]
                                            │
                             ┌──────────────┴──────────────┐
                             │ Is Internet Connected?     │
                             └──────────────┬──────────────┘
                                            │
                     ┌──────────────────────┴──────────────────────┐
                     ▼ YES                                         ▼ NO
        [ POST /api/sync-push ]                       [ Keep in local queue ]
                     │                                             │
      [ Mark last_sync_online = NOW ]                 [ Auto-push on reconnect ]
```

#### How to Use:
1. In **Settings -> Server Settings**, set your **Project URL** (e.g., `https://www.esanshar.com.np`).
2. The sync badge in the top menu shows current cloud status (Online / Offline).
3. You can trigger an immediate full sync at any time via **Settings -> Sync with Live Server**.

#### Business Benefits:
* **No Lost Revenue**: Conduct business uninterrupted during ISP downtime; all sales synchronize automatically once connection restores.
* **Centralized HQ Reporting**: Business owners can monitor multi-branch operations remotely on the web dashboard while front-desk teams work locally.

---

### 5. 🖨️ Thermal POS Receipt & KOT Spooler Integration

#### How It Works:
Communicates directly with Windows print spoolers to output formatted 80mm ESC/POS thermal receipts and kitchen order tickets (KOT).

#### How to Use:
1. Open **Settings -> POS & Hardware Peripherals**.
2. Enable **Auto-Print Customer Receipt** for automatic checkout printing.
3. Enable **Auto-Print Kitchen KOT** so incoming food orders immediately print to your kitchen or bar ticket printers.
4. Custom branding, tax headers, PAN numbers, and footer greetings can be configured under Branding settings.

#### Business Benefits:
* **Rapid Table Turnover**: Generate and print bills in one click.
* **Audit & Tax Ready**: Formatted receipts include VAT, Service Charges, and PAN details compliant with national tax codes.

---

### 6. 📞 Wi-Fi Intercom & WebRTC Guest-to-Staff Calling

#### How It Works:
Leverages local WebRTC audio streaming to create a digital intercom network across your property over Wi-Fi.

#### How to Use:
1. Guests open their room digital menu and tap **Call Reception** or **Request Service**.
2. The Windows desktop app sounds an audio alert and displays an incoming call banner.
3. Reception staff can accept the call to establish real-time, 2-way voice communication directly through their desktop microphone and speakers.
4. **Push-to-Talk (PTT)** mode is available in Settings for busy front-desk environments.

#### Business Benefits:
* **Eliminates PBX Wiring**: Saves hardware wiring and maintenance costs associated with traditional copper intercom systems.
* **Immediate Guest Assistance**: Direct voice communication improves guest satisfaction ratings.

---

### 7. 🏨 Integrated Hotel, Banquet & Restaurant Operations

#### How It Works:
Combines front-desk hotel room management, table bookings, banquet reservations, and food delivery dispatch into a unified interface.

#### Feature Modules Included:
* **Hotel Room Management**: Room rack visualizer, check-in, check-out, folio billing, housekeeping status (Clean, Dirty, Inspected).
* **Table & Dine-in POS**: Visual floor plan map (Available, Occupied, Reserved, Billed), split billing, table transfer.
* **Banquet & Event Management**: Hall scheduling, advance payments, catering menu packages, guest count tracking.
* **Delivery & Takeaway**: Customer phone lookup, driver assignment, dispatch timers, unpaid/paid tracking.

---

## 💻 System Requirements

| Specification | Minimum Specification | Recommended Specification |
| :--- | :--- | :--- |
| **Operating System** | Windows 10 (64-bit, Version 1809 or higher) | Windows 11 (64-bit, latest release) |
| **Processor (CPU)** | Intel Core i3 / AMD Ryzen 3 (2.0 GHz or higher) | Intel Core i5 / AMD Ryzen 5 or higher |
| **Memory (RAM)** | 4 GB | 8 GB or higher |
| **Storage** | 500 MB free space (SSD strongly recommended) | NVMe SSD with 2 GB+ free space |
| **Display Resolution**| 1366 x 768 | 1920 x 1080 (Full HD) |
| **Network** | Wi-Fi / Ethernet router for local device connections | Dedicated Gigabit Wi-Fi 6 Router |
| **Audio** | Standard sound card + speakers | External amplified speakers (for kitchen voice alerts) |
| **Peripherals** | Any Windows-compatible 80mm ESC/POS printer | USB or Network (Ethernet) 80mm Thermal Printer |

---

## 🔧 Step-by-Step Installation & Setup

### Step 1: Install the Application
1. Download [`WindowsApp-Setup-1.5.3.exe`](releases/WindowsApp-Setup-1.5.3.exe).
2. Right-click the executable and select **Run as Administrator**.
3. Follow the installation wizard. The app will install into `C:\Program Files\HospitalityOS` and grant necessary permissions to its local database directory.

### Step 2: Provision Your Web Connection (Mandatory)
1. Launch **HospitalityOS** from your Desktop shortcut.
2. In the setup wizard, input your **Master Web System URL**:
   ```
   https://www.esanshar.com.np
   ```
   *(or your customized organization web address)*.
3. Enter your assigned **License Key / API Key** and authenticate with your staff or administrator account.
4. Click **Connect & Initial Sync** to populate your local database with your restaurant menu items, rooms, tables, and tax configurations.

### Step 3: Configure Local Network & Hardware
1. Ensure the Windows PC is assigned a static local IP on your Wi-Fi router (e.g., `192.168.1.100`).
2. Navigate to **Settings -> POS & Hardware Peripherals** to select your thermal receipt printer.
3. Navigate to **Settings -> Kitchen Voice Announcement (TTS)** to select your voice style and test speaker volume.

---

## 🏗️ Technical Architecture

* **UI Framework**: Flutter Desktop (Windows C++ Runner, Dart 3.11)
* **Application Architecture**: Layered Feature-First Architecture with Riverpod 2.6
* **Local Database Engine**: SQLite 3 via `sqflite_common_ffi`
* **Local Web Server**: Dart Shelf (`shelf`, `shelf_router`, `http_multi_server`)
* **Real-time Engine**: WebSocket Channel + WebRTC P2P Mesh (`dart_webrtc`)
* **Speech Synthesis**: Windows SAPI COM (`SAPI.SpVoice` via UTF-16LE Base64 `-EncodedCommand`)
* **Audio Engine**: `audioplayers` native Windows backend
* **Packaging & Delivery**: NSIS 3.x with solid LZMA compression

---

## 📄 Licensing & Authorization

HospitalityOS Windows Hub is proprietary commercial software.  
Usage requires an active enterprise license associated with your Hospitality Web Management installation. Unlicensed devices or nodes disabled from the central web console will be restricted from accessing local POS and KDS operations.

* **Developer**: Sanshar / Technicguy
* **Official Website**: [https://www.esanshar.com.np](https://www.esanshar.com.np)
* **GitHub Repository**: [https://github.com/technicguy/hostify-win](https://github.com/technicguy/hostify-win)
