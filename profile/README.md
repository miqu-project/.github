# Miqu Project

> **A cohesive, high-performance Wayland desktop ecosystem & native mobile applications.**

Welcome to the official GitHub organization for **Miqu**. Miqu is an ambitious, unified desktop environment engineered for Wayland on Linux, featuring a custom wlroots-based compositor, a dedicated modern C++ application toolkit, a native first-party Linux application suite, and companion Android applications.

---

## 🏛️ Ecosystem Architecture

The Miqu ecosystem is structured across four primary repositories:

| Repository | Role | Technology | Description |
|:---|:---|:---:|:---|
| [**`miquland`**](https://github.com/miqu-project/miquland) | **Compositor & Window Manager** | C++20 / wlroots | GPU-accelerated tiling compositor with dynamic layout engines, exposed overview plugin, and IPC daemon (`miquctl`). |
| [**`miqutoolkit`**](https://github.com/miqu-project/miqutoolkit) | **Shared UI Toolkit** | C++20 / Cairo / Pango | Unified Wayland application toolkit providing declarative widgets, fluid animations, and live theme propagation. |
| [**`miqu-linux-apps`**](https://github.com/miqu-project/miqu-linux-apps) | **Native Desktop Suite** | C++20 / miqutoolkit | Cohesive first-party desktop applications (`miqudesk`, `miqusecure`, `miqumusic`, `miqulauncher`, `miqugallery`, `miqudm`, etc.). |
| [**`miqu-android`**](https://github.com/miqu-project/miqu-android) | **Mobile Applications** | Kotlin / Jetpack Compose | Native Android apps and mobile companions designed to complement the Miqu environment. |

---

## ✨ Key Principles & Vision

- 🎨 **Zero UI Fragmentation**: Rather than relying on mismatched third-party UI frameworks, all desktop applications are powered by `miqutoolkit` for instant theme synchronization, consistent typography, and fluid animation curves.
- ⚡ **Lightweight & High-Performance**: Built from scratch in modern C++ and wlroots, eliminating unnecessary abstraction layers and bloated runtimes.
- 🛡️ **Security & Privacy First**: First-party tooling like `miqusecure` integrates system firewall selection, OpenSnitch rules, LUKS encryption status, and Tor routing directly into an intuitive native interface.
- 🪟 **Intuitive Desktop Ergonomics**: Combines the precision and speed of dynamic tiling window management with an accessible, interactive desktop canvas (`miqudesk`).

---

## 📦 Native Application Suite Overview

- 🖥️ **`miqudesk`** — Interactive desktop canvas & widget layer bringing classic desktop usability into the Wayland tiling environment.
- 🔒 **`miqusecure`** — Privacy and firewall command center (OpenSnitch, Tor, LUKS, audit policies).
- 🎵 **`miqumusic`** — High-efficiency, lightweight native MPD client and audio player.
- 🚀 **`miqulauncher`** — Fuzzy application launcher, dmenu alternative, and workspace/window switcher.
- 👁️ **`miquoverview`** — GPU-accelerated live workspace expose and overview plugin for `miquland`.
- 🖼️ **`miqugallery`** — Minimalist, responsive image viewer and media gallery.
- 📊 **`miquinfo`** — System telemetry, hardware resource monitor, and diagnostic dashboard.
- 🚪 **`miqudm`** — Wayland-native Display Manager & greeter with PAM/logind session integration.
- 🔐 **`miqulock` & `miquidle`** — Protocol-compliant session locking (`ext-session-lock`) and idle management.

---

## 🛠️ Community & Ecosystem

- 🌐 **Organization**: [github.com/miqu-project](https://github.com/miqu-project)
- 💡 **Contribute**: Feel free to explore our repositories, report issues, and submit pull requests.

---

<p align="center">
  <sub>Built with passion for the Linux and Wayland community.</sub>
</p>
