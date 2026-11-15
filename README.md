# ✈️ Geo-FS Pushback Add-On

A lightweight pushback project for GeoFS, with a browser-based JavaScript bookmarklet and a separate Java desktop simulator.

The idea is simple: give pilots a more convenient way to simulate aircraft pushback without loading a bunch of extra models, libraries, or heavy scripts.

This project has two editions:

- **JavaScript Bookmarklet** – designed to run directly inside GeoFS through your browser.
- **Java Edition** – a standalone desktop simulator that demonstrates pushback controls through a Java console.

Both editions are designed to stay relatively lightweight and easy to understand.

---

## 📌 Project Features

### 🌐 JavaScript Bookmarklet

The bookmarklet is designed for use inside GeoFS.

Current Lite features:

- Floating pushback control panel.
- Adjustable pushback speed.
- Start and Stop controls.
- GeoFS aircraft detection.
- Basic ground-contact checks before starting.
- Automatic cleanup when the panel is closed.
- Lightweight operation without downloading external 3D models.
- No Tampermonkey requirement.
- Designed with browser use in mind, including iPad Safari.

The Lite edition intentionally leaves out the original 3D pushback truck to reduce extra loading and complexity.

### ☕ Java Edition

The Java edition is a separate desktop simulator.

It includes:

- Start and Stop commands.
- Adjustable pushback speed.
- Yaw adjustment.
- Status reporting.
- Speed limits.
- Yaw limits.
- Simple command-based operation.

**Important:** The Java edition does not directly control GeoFS. It is a standalone demonstration of pushback logic and controls, not a GeoFS plugin.

---

## 🧠 How the Bookmarklet Works

The bookmarklet is written in JavaScript and runs inside the browser page where GeoFS is open.

Unlike a traditional userscript, it does not require Tampermonkey or another userscript manager. It is saved as a browser bookmark with JavaScript as its address.

### 1. GeoFS Detection

When the bookmarklet is launched, it checks whether GeoFS has exposed the aircraft and physics objects that the script needs.

It looks for important objects such as:

- `geofs.aircraft.instance`
- `geofs.animation.values`
- The aircraft rigid-body physics interface.
- The aircraft heading value.

If those objects are unavailable, the bookmarklet displays an error instead of attempting to run.

### 2. Control Panel Creation

After the required objects are detected, the bookmarklet creates a small floating panel directly on the GeoFS page.

The panel contains:

- Pushback speed slider.
- Current speed display.
- Start button.
- Stop button.
- Close button.
- Status display.

The panel is created dynamically, so there is no separate HTML file to install.

### 3. Speed Control

The speed slider allows the user to select a pushback speed between 0.5 and 4.0.

The selected value is stored in the script and used while pushback is active.

### 4. Aircraft Movement

When Start is pressed, the bookmarklet checks that the aircraft is on the ground and is not already moving above the allowed threshold.

It then uses the aircraft's heading to calculate a movement direction.

The script applies a velocity through GeoFS's exposed rigid-body interface:

`setLinearVelocity()`

The current Lite implementation updates the velocity approximately every 100 milliseconds while active.

This is intended to keep the script from running an unnecessarily frequent update loop.

### 5. Stopping and Cleanup

When Stop is pressed, the bookmarklet clears its update interval and attempts to stop the pushback movement.

When Close is pressed, it also removes the floating control panel.

Running the bookmarklet again while its panel is open also closes the panel and stops its active timer.

### 6. Lightweight Design

The Lite edition deliberately avoids:

- External model downloads.
- Additional 3D pushback truck rendering.
- Large external JavaScript libraries.
- Unnecessary background update loops.
- Direct changes to Cesium rendering settings.

The bookmarklet does not disable or replace the GeoFS Cesium renderer. GeoFS remains responsible for its own scenery and graphics rendering.

---

## ☕ How the Java Edition Works

The Java edition is designed as a standalone command-line pushback simulator.

It does not run inside the GeoFS browser page. Instead, it uses Java to demonstrate how a basic pushback control system can be organised.

### 1. Starting the Program

When the Java application launches, it displays a command prompt where the user can enter pushback commands.

The program waits for commands and processes them through its command-handling logic.

### 2. Available Commands

| Command | Function |
|---|---|
| `START` | Starts the simulated pushback |
| `STOP` | Stops the simulated pushback |
| `SPEED 5` | Sets the simulated speed to 5.0 |
| `YAW 10` | Sets the yaw value to 10 degrees |
| `STATUS` | Displays the current simulator status |
| `EXIT` | Closes the program |

### 3. Speed Management

The Java version stores the selected pushback speed as a numerical value.

It checks the requested value against its configured speed limit, which is 20.0.

This prevents the simulator from accepting values outside its defined range.

### 4. Yaw Management

Yaw represents the simulated turning angle.

The Java version limits yaw to a range between -30 and +30 degrees.

This allows the program to demonstrate basic directional control without accepting unlimited values.

### 5. Status Reporting

The `STATUS` command reports information about the simulator, including whether pushback is active and the current speed and yaw settings.

### 6. Standalone Operation

The Java edition does not need GeoFS, a browser, Cesium, or a 3D model to run.

It is a separate learning and simulation project.

---

## 📥 Installation

### Bookmarklet Installation

The bookmarklet is intended for browsers that support JavaScript bookmarklets.

1. Open GeoFS in your browser.
2. Create a new browser bookmark.
3. Give it a name, such as `GeoFS Pushback Lite`.
4. Edit the bookmark.
5. Replace its URL/address field with the complete bookmarklet code.
6. Save the bookmark.
7. Return to GeoFS.
8. Select the bookmark to launch the panel.

**iPad Safari:** You can save the bookmark through Safari's bookmark editor. The exact editing steps can vary slightly by iPadOS version.

### Java Installation

1. Install a Java Development Kit (JDK).
2. Save the Java source file.
3. Open a terminal in the directory containing the file.
4. Compile the program.
5. Run the compiled application.

Example commands, assuming the source file is named `PushbackSimulator.java`:

```bash
javac PushbackSimulator.java
java PushbackSimulator
```

---

## 🖥️ Compatibility

| Platform | Bookmarklet | Java Edition |
|---|---|---|
| Windows | Browser-dependent | Yes, with Java |
| macOS | Browser-dependent | Yes, with Java |
| iPad Safari | Intended target | No direct browser integration |
| GeoFS 4.0 Beta | Experimental | Not connected |
| Desktop browsers | Intended target | Separate application |

**Compatibility note:** GeoFS 4.0 Beta uses internal JavaScript objects that may change between updates. The bookmarklet's compatibility is experimental and has not been independently verified across every aircraft, browser, or GeoFS version.

---

## ⚙️ Design Philosophy

This project aims to keep pushback controls straightforward.

The browser edition focuses on:

- Low overhead.
- Simple controls.
- No external model downloads.
- Minimal page modifications.
- Easy bookmark-based installation.

The Java edition focuses on:

- Simple command handling.
- Input validation.
- Speed and yaw limits.
- Readable standalone simulation logic.

The two editions share the same general pushback concept, but they operate independently.

---

## 🚧 Current Limitations

The current Lite bookmarklet is not a complete recreation of the original pushback userscript.

Features not included in the current Lite build:

- 3D pushback truck model.
- Aircraft-specific truck positioning.
- Truck animation.
- Separate tug steering and yaw controls.
- Full forward and reverse control system.
- A dedicated aircraft compatibility database.

The original userscript included more advanced truck and aircraft-specific features. Those features were left out of the Lite conversion to avoid additional model loading and complexity.

The Java edition is a standalone simulator and does not control an aircraft in GeoFS.

---

## 🔮 Possible Future Improvements

Ideas for future versions:

- Aircraft-specific pushback support.
- Optional pushback truck visuals.
- Improved steering controls.
- Better touch controls for iPad.
- More detailed aircraft compatibility checks.
- Improved movement handling.
- A graphical interface for the Java edition.
- A shared visual design between both editions.

These are ideas for future development, not features currently guaranteed to be available.

---

## 📜 License

This project is intended to be released under the **MIT License**.

You may use, modify, and distribute the code in accordance with the license terms.

---

## ⚠️ Warning & Disclaimer

This is an independent community project and is not affiliated with GeoFS or its developers.

The bookmarklet interacts with internal GeoFS browser objects. Changes to GeoFS may cause it to stop working or behave differently.

Use the bookmarklet carefully, especially while operating an aircraft in the simulator. Stop the aircraft before attempting pushback.

The Java edition is a standalone demonstration and does not connect to GeoFS.

**Use at your own discretion. Compatibility and functionality may vary depending on the software version and browser.**

---

*Made for aviation enthusiasts who enjoy experimenting with GeoFS and building their own tools.* ✈️
