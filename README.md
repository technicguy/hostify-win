# HospitalityOS (HOSTIFY) — Windows Desktop App (Offline Hub)

[![Platform](https://img.shields.io/badge/Platform-Windows%2010%20%7C%2011%20(x64)-blue.svg)](#system-requirements)
[![Release](https://img.shields.io/badge/Release-v1.5.3-emerald.svg)](releases/WindowsApp-Setup-1.5.3.exe)
[![Architecture](https://img.shields.io/badge/Engine-Flutter%203.41%20%7C%20Dart%203.11-cyan.svg)](#technical-architecture)
[![License](https://img.shields.io/badge/License-Proprietary%20%2F%20Commercial-amber.svg)](#licensing--authorization)

![HOSTIFY HospitalityOS](hostify.png)

> **HOSTIFY HospitalityOS Offline Hub** is the comprehensive enterprise desktop operations center for hotels, resorts, multi-outlet restaurants, and banquet venues. It functions as an **autonomous edge server & POS terminal** that guarantees non-stop front-desk, dining, kitchen, and billing operations — **even during complete internet and cloud outages**.

---

## ⚠️ MANDATORY DEPENDENCY & PREREQUISITE NOTICE

> [!CAUTION]
> ### 🛑 Without the Hospitality Web System, This Desktop Version WILL NOT Work!
> 
> **HOSTIFY Windows Desktop is NOT an independent or standalone offline software.**  
> It is an **offline edge node / local operations hub** that is intrinsically bound to your **Hospitality Management Web System** (hosted on `https://www.esanshar.com.np` or your private dedicated domain).
>
> 1. **Initial Provisioning & Authentication**: On first launch, you **CANNOT** use the software without linking your **Project Base URL** and signing in with an authorized staff or administrator account created on your web system.
> 2. **Master Catalog Authority**: Your food menu, categories, room inventories, room types, banquet halls, tax rules (VAT/PAN), and user privileges originate from and are maintained by the web platform.
> 3. **Hardware Fingerprint & Node Authorization**: The app submits a unique machine fingerprint (`desk_<hostname>_<hash>`) to the Mother Licensing Authority on the web system. If an administrator disables access for this node, POS and KDS operations are locked.
> 4. **Bidirectional Ledger Synchronization**: Offline transactions (bookings, table orders, payments, room folios) are queued locally and **must be synced** back to the web platform to maintain consolidated business accounts.

---

## 📥 Download Latest Official Release

| Installer File | Version | Architecture | SHA256 Checksum | Direct Download |
| :--- | :---: | :---: | :--- | :--- |
| **`WindowsApp-Setup-1.5.3.exe`** | `v1.5.3` | `x64` (64-bit) | `19FE9F26C036F6A6F416134B15ACCB1A1E081643596577D488B921463F790DE8` | [⬇️ Download Installer (21.0 MB)](releases/WindowsApp-Setup-1.5.3.exe) |

---

## 📑 Complete In-App User Guide & Module Documentation

This documentation directly mirrors the comprehensive **Documentation & User Guide** built into the HOSTIFY Desktop Hub application.

```
========================================================================================
                          HOSTIFY DESKTOP HUB MODULE DIRECTORY
========================================================================================
 1. GETTING STARTED            2. HOTEL MANAGEMENT           3. RESTAURANT & POS
    • About HOSTIFY               • Hotel Bookings & Folios     • Tables & Menu Catalog
    • Login & First-Time Setup    • Occupancy Calendar & Rack   • Take-Order POS Terminal
    • Navigating the UI Workspace • Rooms & Housekeeping        • Kitchen Display (KDS) + TTS
    • Operations Dashboard        • Guests Directory & Wallet   • Billing, Payments & Deposits
                                                                • All Orders & Receipts
 4. GUEST & STAFF MOBILITY     5. OPERATIONS & EVENTS        6. ADMINISTRATION & HELP
    • Guest QR Digital Menu       • Delivery Dispatch System    • User Roles & Permissions
    • Staff Mobile App Gateway    • Banquets & Event Halls      • Offline Sync Engine & Backup
    • Wi-Fi WebRTC Intercom       • Finance, Invoices & Reports • Settings, POS Hardware & Diagnostics
                                                                • Frequently Asked Questions (FAQ)
                                                                • Troubleshooting & System Glossary
========================================================================================
```

---

### 1. 🚀 Getting Started

#### 1.1 About HOSTIFY
* **Overview**: HOSTIFY is a full-spectrum hospitality management solution combining Hotel PMS, Restaurant POS, Banquet Coordinator, and Delivery Dispatch.
* **The Desktop Hub Role**: The desktop application is the local nerve center:
  * Manages the high-speed local SQLite database (`sqflite_common_ffi`).
  * Runs a self-contained local web server (`:8090` HTTP / `:8443` HTTPS) for staff mobile apps and guest QR menus.
  * Synchronizes bidirectionally with the central web platform when internet access is available.

#### 1.2 Login & First Setup
* **Location**: Login Screen → Settings → System & Hardware
* **Step-by-Step Setup**:
  1. Launch HOSTIFY on Windows and sign in with your staff credentials (assigned via the web system).
  2. In **Settings → System & Hardware**, verify your **Live Server URL** (e.g., `https://www.esanshar.com.np`) and **API License Key**.
  3. Click **Backup / Sync** in the top ribbon to pull down your complete master catalog: food menus, table layouts, room classifications, and staff directories.
  4. Navigate to **Restaurant Management → Tables** and **Hotel Management → Rooms** to verify your data has been seeded into local storage.
  5. Check **Connectivity → Device Connectivity (Staff)** to view the local IP address for mobile devices.
* **Important Note**: The initial provisioning requires internet connectivity. Once completed, the workstation operates completely offline.

#### 1.3 Navigating the App Workspace
* **Top Quick-Action Ribbon**: One-click navigation shortcuts to *Hotel Bookings, Guests, Tables/Rooms, POS, Food Menu, Delivery, KDS, Reports, Backup, Settings*.
* **Status Bell & Alerts**: Real-time notifications for local database integrity, sync queue status, and new orders.
* **Orange Call Banner**: Real-time alert banner that triggers whenever a guest clicks *"Call Staff"* or initiates an intercom call from their table or room.
* **Collapsible Left Sidebar**: Categorized access to all system modules (Dashboard, Hotel, Restaurant, Finance, Inventory, Connectivity, Settings).

#### 1.4 Live Dashboard
* **Location**: Sidebar → Dashboard
* **Features & Metrics**:
  * Live occupancy indicators for both hotel rooms and dining tables (Available, Occupied, Reserved, Dirty).
  * Real-time counters of active kitchen orders (Pending, Preparing, Completed).
  * Quick shortcuts into reservation entry, POS checkout, and financial revenue summaries.

---

### 2. 🏨 Hotel Management Suite

#### 2.1 Room Bookings, Calendar & Folios
* **Location**: Sidebar → Hotel Management → Bookings / Calendar
* **Sub-Modules**:
  * **Bookings Ledger**: Create, modify, check in, and check out guest reservations.
  * **Visual Calendar**: Color-coded timeline matrix displaying real-time room occupancy and future reservations across dates.
  * **Rooms Directory**: Room list with real-time operational states (*Available, Occupied, Dirty, Maintenance*).
  * **Room Types**: Classification rules, default pricing, and bed configurations.
  * **Extra Services**: Billable add-ons including laundry, airport transfers, mini-bar restocking, and extra bedding.
* **Creating a Reservation**:
  1. Go to **Hotel Management → Bookings** and click **New Booking**.
  2. Select an existing guest from the directory or create a new profile with ID verification details.
  3. Select check-in and check-out dates; available rooms are filtered automatically.
  4. Record an advance deposit payment if applicable (cash, card, bank QR, or guest wallet).
  5. Save to reserve the room on the master timeline.
* **Guest Check-Out & Folio Settlement**:
  1. Open the active booking and select **Check-out**.
  2. The consolidated folio automatically compiles room tariffs, extra services, and room-service food orders charged to the room.
  3. Deduct any advance deposits, select the final settlement payment method, and generate the official GST/VAT invoice.
  4. Upon check-out, the room status shifts to **Dirty** to alert housekeeping.

#### 2.2 Guests Directory & Deposit Wallet
* **Location**: Sidebar → Guests Directory (or Ribbon → Guests)
* **Capabilities**:
  * Instant guest search by full name, mobile number, or government identity/passport number.
  * Detailed history of past visits, room preferences, and lifetime spending.
  * **Guest Deposit (Wallet) System**: Manage prepaid customer credit balances that can be redeemed across dining, room charges, and banquet bookings.

---

### 3. 🍽️ Restaurant Management & POS Terminal

#### 3.1 Tables & Menu Items Catalog
* **Location**: Sidebar → Restaurant Management → Tables / Menu Items
* **Table Layouts**: Define dining areas, outdoor patios, VIP lounges, and individual table capacities. Enable or disable self-service QR ordering per table.
* **Visual Table Status Matrix**:
  | Status | Color Indicator | Meaning & Workflow |
  | :--- | :---: | :--- |
  | **Available** | Green | Table is vacant and ready for new guests. |
  | **Occupied** | Blue | Table currently has active, unbilled orders. |
  | **Reserved** | Purple | Table is booked for an upcoming reservation. |
  | **Dirty** | Orange | Table requires bussing/cleaning before re-seating. |
* **Menu Items Management**: Maintain food and drink items with multi-tier pricing, category tags, tax configurations, and photos. Quickly toggle items off when out of stock.

#### 3.2 POS: Taking Orders
* **Location**: Ribbon → POS, or click any table → Take Order
* **Workflow**:
  1. Click **POS** and select the designated Table or Hotel Room.
  2. Tap categories and menu items to assemble the cart.
  3. Specify preparation modifiers and special dietary notes (e.g., *"extra spicy"*, *"no onions"*).
  4. Submit order: Instantly broadcasts to the Kitchen Display System (KDS) and prints the Kitchen Order Ticket (KOT).
* **Multi-Order Support**: Multiple separate orders (e.g., drinks first, main course later) can be submitted under a single table. They are automatically consolidated onto a single master bill.

#### 3.3 Kitchen Display System (KDS) & Voice TTS Announcements
* **Location**: Ribbon → KDS, or Restaurant Management → Active Orders (KDS)
* **KDS Workflow Columns**:
  * **Pending**: New incoming orders awaiting kitchen acceptance. Triggers audio chime and voice announcements.
  * **Preparing / In Progress**: Kitchen chefs have acknowledged and started cooking.
  * **Completed**: Food has been plated and dispatched.
* **Native Windows Speech Synthesis (SAPI.SpVoice)**:
  * Converts order details into spoken audio alerts using Windows native TTS — **no cloud APIs, no internet, zero lag**.
  * **Detailed Mode**: Announces table/room and exact items (*"New order for Table 3. 2 Chicken Burger, 1 Lemon Tea."*).
  * **Compact Mode**: Summary announcement (*"New order for Table 3. 3 items."*).
  * **Alert Only**: Urgent audio alert (*"New order received."*).
* **Full Item Visibility**: Cards display all items, modifier notes, and quantity badges (`1x`, `2x`) with no hidden truncation.
* **Completed ≠ Paid**: Kitchen completion indicates food service only. The order remains active on the table bill until settled by the cashier.

#### 3.4 Billing, Payments & Deposit Settlements
* **Location**: Occupied Table → Order Tab → Payment
* **Payment Statuses**:
  * **Unpaid**: Order placed; remains open on table bill.
  * **Partial**: Portion paid; balance remains due.
  * **Credit / Due**: Ledger balance charged to customer account for deferred settlement.
  * **Paid**: Full balance settled; order moves to archive and table returns to Available.
* **Guest Wallet Redemptions**: Apply customer advance deposits directly against dining charges with one click.

#### 3.5 All Orders & Receipts Archive
* **Location**: Sidebar → Restaurant Management → All Orders
* **Capabilities**:
  * Search past orders by order ID, date range, table number, customer name, or payment status.
  * Re-open and reprint thermal receipts or KOT duplicates.
  * Fully accessible offline from the local SQLite database.

---

### 4. 📱 Guest & Staff Mobility (Local Network)

#### 4.1 Guest Digital QR Menu
* **How It Works**:
  * The desktop application hosts an in-house web server on port `8090` (HTTP) and `8443` (HTTPS).
  * Guests scan the QR code at their table or in their room using any smartphone camera.
  * Menus open immediately in their mobile browser without downloading an app.
  * Guests can add items, review prices, submit orders, and track preparation status in real time.
  * A **Call Staff** button sends an alert to the desktop app with an audio prompt.
* **Network Requirement**: Guest smartphones must be connected to the venue's local Wi-Fi router.

#### 4.2 Staff Mobile App Gateway
* **Location**: Sidebar → Connectivity → Device Connectivity (Staff)
* **Waitstaff Mobile Functionality**:
  * Waitstaff connect Android or iOS devices over local Wi-Fi using the displayed IP address (or by scanning the connectivity QR code).
  * Staff take orders tableside; submissions sync directly into the desktop SQLite database.
  * Table status changes update simultaneously across all mobile and desktop screens.

#### 4.3 WebRTC Voice Intercom
* Enables low-latency, two-way audio calls between guest devices (table/room) and the desktop front-desk terminal over local Wi-Fi without internet or PBX hardware.
* Push-to-Talk (PTT) mode is available in Settings for front-desk environments.

---

### 5. 🎯 Operations, Banquets & Delivery

#### 5.1 Delivery Management
* **Location**: Sidebar → Delivery Management (or Ribbon → Delivery)
* **Workflow**: Record customer phone, delivery address, ordered items, and delivery fee. Assign delivery personnel, track status (*Pending → Dispatched → Delivered*), and reconcile driver cash collection.

#### 5.2 Banquet & Event Hall Management
* **Location**: Sidebar → Banquets Management
* **Sub-Modules**:
  * **Halls & Venues**: Define event spaces, seating capacities, and hourly/daily rental rates.
  * **Hall Bookings**: Reserve venues with event schedules, estimated guest counts, and advance deposits.
  * **Catering Packages & Add-ons**: Attach food buffets, audio-visual equipment, and decorative extras to event folios.

#### 5.3 Finance, Invoices & Accounting
* **Location**: Sidebar → Finance / Accounting
* **Capabilities**:
  * View sales invoices and record payments against them.
  * Financial reports by date, payment method (Cash, Card, QR, Credit), and revenue center.
  * Generate accounting vouchers that sync with the cloud general ledger.

---

### 6. ⚙️ Administration, Sync & Troubleshooting

#### 6.1 User Management & Role Permissions
* **Location**: Sidebar → User Management
* **Staff Access Control**: Create staff logins with specific permission profiles (Admin, Cashier, Waitstaff, Kitchen Chef). Control which screens and actions each role can access.

#### 6.2 Offline Storage, Sync & Cloud Backup
* **Location**: Ribbon → Backup, or Sidebar → Connectivity
* **The Offline-First Principle**:
  1. Every action (booking, order, payment) is saved to the local SQLite database first.
  2. Offline entries are flagged for cloud upload.
  3. Clicking **Backup** pushes local changes to the cloud web system and downloads any updates made remotely.
  4. If internet connectivity drops, operations continue without interruption; sync resumes once connectivity is restored.

#### 6.3 Hardware Peripherals & Settings
* **Location**: Sidebar → Settings
* **Configuration Options**:
  * **POS Printers**: Configure 80mm ESC/POS thermal printers via Windows print spoolers.
  * **Auto-Printing**: Automatically print customer receipts on checkout and KOTs on order placement.
  * **Branding & Tax**: Configure business headers, PAN/VAT registration numbers, and custom receipt footers.
  * **Diagnostics & Health**: Monitor local server port status, SQLite table row counts, and connectivity latency.

---

## ❓ Frequently Asked Questions (FAQ)

> **Q: Can I use this desktop app if my business does not have the HOSTIFY website?**  
> **A: NO.** The desktop version requires the cloud web system for initial setup, licensing, menu catalogs, and user authorization.

> **Q: What happens if our internet connection goes down during service?**  
> **A: Operations continue normally.** Table orders, KDS kitchen tickets, thermal printing, and room check-ins run through the local database and local Wi-Fi. Sync with the cloud resumes automatically when the internet returns.

> **Q: How do guest phones access the digital menu without an internet connection?**  
> **A: Via your local Wi-Fi router.** The desktop app runs an embedded web server on port `8090`/`8443`. As long as guest phones are connected to the venue Wi-Fi, they can open the menu directly from the desktop computer.

> **Q: An order is marked "Completed" on the KDS, but the table still shows Occupied. Why?**  
> **A: Kitchen completion and billing are separate.** "Completed" means the kitchen has finished preparing the food. The table remains Occupied until the bill is settled through Payment.

> **Q: Where is my data saved?**  
> **A: Locally on your PC and in the cloud.** All operational data is stored in the local SQLite database on your computer's drive and replicated to your secure cloud web system during sync.

---

## 💻 System Requirements

| Component | Minimum Specification | Recommended Specification |
| :--- | :--- | :--- |
| **Operating System** | Windows 10 (64-bit, Version 1809+) | Windows 11 (64-bit, latest release) |
| **Processor (CPU)** | Intel Core i3 / AMD Ryzen 3 (2.0 GHz) | Intel Core i5 / AMD Ryzen 5 or higher |
| **Memory (RAM)** | 4 GB | 8 GB or higher |
| **Storage** | 500 MB free space (SSD recommended) | NVMe SSD with 2 GB+ free space |
| **Display Resolution**| 1366 x 768 | 1920 x 1080 (Full HD) |
| **Networking** | Wi-Fi / Ethernet router for local devices | Dedicated Gigabit Wi-Fi 6 Router |
| **Audio** | Standard audio output | External speakers (for kitchen voice announcements) |
| **Receipt Printer** | Windows-compatible 80mm ESC/POS printer | USB or Ethernet (LAN) 80mm Thermal Printer |

---

## 🏗️ Technical Architecture

* **UI Framework**: Flutter Desktop (Windows C++ Runner, Dart 3.11)
* **State Management**: Riverpod 2.6 (`StateNotifierProvider`)
* **Local Database Engine**: SQLite 3 via `sqflite_common_ffi`
* **Local Server**: Dart Shelf Framework (`shelf`, `shelf_router`, `http_multi_server`)
* **Real-time Networking**: WebSocket Channels + WebRTC P2P Mesh (`dart_webrtc`)
* **Voice Synthesis Engine**: Windows Native SAPI (`SAPI.SpVoice` via UTF-16LE Base64 PowerShell execution)
* **Audio Engine**: `audioplayers` native Windows backend
* **Packaging**: NSIS (Nullsoft Scriptable Install System) v3.x with LZMA compression

---

## 📄 Licensing & Authorization

HospitalityOS Windows Hub is proprietary commercial software.  
Usage requires an active enterprise license tied to your Hospitality Web Management installation. Unlicensed instances or nodes disabled from the central web console will be restricted from accessing local POS and KDS operations.

* **Developer**: Sanshar / Technicguy
* **Official Website**: [https://www.esanshar.com.np](https://www.esanshar.com.np)
* **GitHub Repository**: [https://github.com/technicguy/hostify-win](https://github.com/technicguy/hostify-win)
