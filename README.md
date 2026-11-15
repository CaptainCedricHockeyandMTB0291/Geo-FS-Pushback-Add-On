# ✈️ Geo-FS Pushback Add-On

### An independent pushback project for GeoFS featuring a JavaScript bookmarklet and a standalone Java edition.

Welcome to Geo-FS Pushback!

This project is designed to bring a pushback-style control interface to GeoFS, with adjustable speed, steering controls and a simple interface for desktop and mobile users.

The goal is to keep things lightweight, easy to use and expandable for future development.

---

## 🧰 Features

- 🎮 **Pushback Control Panel** — A compact browser-based interface.
- ⚡ **Adjustable Speed** — Change the pushback speed value.
- ↔️ **Steering Controls** — Adjust steering and yaw.
- ◀️ **Left / Right Controls** — Quick steering buttons.
- 🛑 **Stop Button** — Reset the current controls.
- 💻 **Java Edition** — A separate desktop-based simulator.
- 📱 **Mobile-Friendly Interface** — Designed with touch-screen use in mind.

## 🌐 Supported Platforms

| Platform | Format |
|---|---|
| Windows | Java / Bookmarklet |
| Microsoft Edge | Bookmarklet |
| Google Chrome | Bookmarklet |
| iPad | Safari Bookmarklet |
| macOS | Java / Bookmarklet |

Some browsers have restrictions on bookmarklets, so compatibility may vary depending on the device.

## 📦 Installation

### 🌍 Bookmarklet Edition

1. Open your browser's bookmark manager.
2. Create a new bookmark.
3. Name it `GeoFS Pushback`.
4. Edit the bookmark.
5. Paste the bookmarklet code into the URL field.
6. Save the bookmark.
7. Open GeoFS and activate it.

### ☕ Java Edition

Make sure Java is installed on your computer.

Compile:

```bash
javac GeoFSPushback.java
```

Run:

```bash
java GeoFSPushback
```

The Java version runs independently and does not connect directly to GeoFS.

## ⚙️ How It Works

The JavaScript version creates a control panel inside the browser, with sliders and buttons for adjusting the pushback settings.

The Java version provides a command-line interface where users can change speed, steering and other settings.

Both editions are separate, so you can use the version that suits your setup.

**Important:** The current bookmarklet is a control-panel prototype. Its controls do not yet move the aircraft in GeoFS. Live aircraft integration and truck
