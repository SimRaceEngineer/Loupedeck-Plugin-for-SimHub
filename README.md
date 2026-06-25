# Full Loupedeck Live Plugin for SimHub

[![Support on Ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/simrace)

Turn your **Loupedeck Live** (or **Razer Stream Controller**) into a complete SimHub control
surface — icons on every key, live telemetry, 8 pages, dials, and a one-click mirror of your
SimHub **Control Mapper**.

> Tested on the Loupedeck Live / Razer Stream Controller (VID 1532 / PID 0D06, firmware 0.2.x).

---

## Features

- **🪞 Control Mapper mirror** — assign any of your game-control roles (Pit Request, ABS±, ARB±,
  brake bias, TC, diff…) to a key **by name**. The plugin presses the matching vJoy output button —
  exactly like a wheel button mapped in the Control Mapper. Your roles are read **automatically**
  from your active Control Mapper config (zero setup).
- **🎨 Icons** on the 12 touch tiles **and** on the 6 dials (side strips). Browse your own icon
  library (any PNG pack) with a folder tree + name search.
- **📄 8 pages** — the 8 round buttons switch pages, each with its own 12 tiles + 6 dials (up to
  240 assignments). **Copy a page** to another in one click.
- **📊 Live telemetry on tiles** — RPM, speed, gear, temperatures, fuel… Pick any SimHub property
  from a searchable browser that shows each property's **live value**.
- **🎛️ 6 dials** — each direction (CW / CCW) and the click can trigger a Control Mapper role or a
  plugin action.
- **📳 Haptic feedback** on press.
- Also exposes named inputs (**Loupedeck Tile N / Dial N / Button N**) bindable in
  *SimHub → Controls & events* for plugin actions.

---

## Install

1. **Quit the Loupedeck software** (system tray → *Quit*) — it must release the device.
2. Download **`LoupedeckSimHub.dll`** from the [latest release](../../releases) and drop it into
   your SimHub installation folder.
3. Restart SimHub and **enable** the *Loupedeck* plugin when prompted.
4. Open the **Loupedeck** tab to configure.

## Setup

- **Icons** — *Dossier d'icônes → Changer…* and point to your Stream Deck / PNG icon folder.
- **Roles** — loaded automatically from your active Control Mapper. They press the vJoy device your
  Control Mapper outputs to, so set your Control Mapper **output to vJoy** and make sure your game
  reads that vJoy device. Requires [vJoy](https://github.com/jshafer817/vJoy).
- **Pages** — press the round buttons to switch; configure each page in the panel. Use *Copier
  depuis : Page X* to duplicate a page.

## Notes

- Icons are **not** bundled — use any Stream Deck icon pack you already own and point the plugin to
  its folder.
- The Loupedeck software and this plugin can't use the device at the same time (one owns the USB
  serial port). Quit the Loupedeck software while racing.

---

If this plugin saves you time, you can support development here:

[![Support on Ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/simrace)
