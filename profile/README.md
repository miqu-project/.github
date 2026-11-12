<p align="center">
  <img src="https://raw.githubusercontent.com/miqu-project/.github/main/assets/logo.png" alt="Miqu Project Logo" width="180" />
</p>

<h1 align="center">Miqu Project</h1>

<p align="center">
  <b>A cohesive, high-performance Wayland desktop ecosystem & native mobile applications.</b><br>
  Website: <a href="https://miqu-project.github.io"><b>miqu-project.github.io</b></a> • Monorepo: <a href="https://github.com/miqu-project/miqu"><b>miqu-project/miqu</b></a>
</p>

<p align="center">
  <a href="https://github.com/miqu-project/miqu"><img src="https://img.shields.io/badge/Monorepo-miqu-red?style=flat-square" alt="miqu" /></a>
  <a href="https://miqu-project.github.io"><img src="https://img.shields.io/badge/Website-miqu--project.github.io-emerald?style=flat-square" alt="Website" /></a>
  <img src="https://img.shields.io/badge/Language-C%2B%2B20-blue?style=flat-square" alt="C++20" />
  <img src="https://img.shields.io/badge/Display-Wayland-orange?style=flat-square" alt="Wayland" />
</p>

---

### What is Miqu?
Miqu is an independent desktop ecosystem engineered from scratch for Wayland on Linux. It eliminates UI fragmentation by pairing a custom wlroots tiling compositor with a dedicated C++20 UI framework (`miqutoolkit`), a modular shell, and native first-party applications.

Our primary portal for full architectural guides, screenshots, and documentation is **[miqu-project.github.io](https://miqu-project.github.io)**.

### Quick Start
Build and install the entire desktop ecosystem in one command:
```bash
git clone https://github.com/miqu-project/miqu.git
cd miqu
sudo ./install.sh
```

---

### What is What

All desktop subsystems and companion apps are organized within our primary monorepo [**`miqu`**](https://github.com/miqu-project/miqu):

- **Core Engine & Framework**
  - [**`miquland`**](https://github.com/miqu-project/miqu/tree/main/miquland): High-performance wlroots Wayland compositor with scenefx GPU blur, dynamic tiling, and `miquctl` IPC.
  - [**`miqutoolkit`**](https://github.com/miqu-project/miqu/tree/main/miqutoolkit): Shared C++20 UI framework with Cairo/Pango vector rendering, RAII safety, and live inotify theme reload.

- **Desktop Shell (`shell/`)**
  - [**`miqubar`**](https://github.com/miqu-project/miqu/tree/main/shell/miqubar): Status bar & taskbar with workspace indicators, system tray, and flyouts.
  - [**`miqudesk`**](https://github.com/miqu-project/miqu/tree/main/shell/miqudesk): Interactive desktop canvas with desktop icons and widgets.
  - [**`miqulauncher`**](https://github.com/miqu-project/miqu/tree/main/shell/miqulauncher): Fast fuzzy application launcher and active window switcher.
  - [**`miquoverview`**](https://github.com/miqu-project/miqu/tree/main/shell/miquoverview): GPU-accelerated workspace exposé and window manager plugin.
  - [**`miqunotify`**](https://github.com/miqu-project/miqu/tree/main/shell/miqunotify): Native desktop notification daemon and slide-out center.
  - [**`miqupower`**](https://github.com/miqu-project/miqu/tree/main/shell/miqupower): Session and power management dialog with running application guards.
  - [**`miqudm`**](https://github.com/miqu-project/miqu/tree/main/shell/miqudm): Wayland-native Display Manager and login greeter (PAM/logind).
  - [**`miqubg`**](https://github.com/miqu-project/miqu/tree/main/shell/miqubg): Wallpaper daemon with smooth multi-monitor scaling and transitions.
  - [**`miqulock`**](https://github.com/miqu-project/miqu/tree/main/shell/miqulock) & [**`miquidle`**](https://github.com/miqu-project/miqu/tree/main/shell/miquidle): Protocol-compliant screen locker (`ext-session-lock-v1`) and idle daemon (`ext-idle-notify-v1`).
  - [**`miqupolkit`**](https://github.com/miqu-project/miqu/tree/main/shell/miqupolkit): Graphical Polkit agent for privilege escalation prompts.

- **Desktop Applications (`apps/`)**
  - [**`miqucontrolpanel`**](https://github.com/miqu-project/miqu/tree/main/apps/miqucontrolpanel): Centralized settings manager, WireGuard VPN, Private DNS (DoT), and privacy center.
  - [**`miqufiles`**](https://github.com/miqu-project/miqu/tree/main/apps/miqufiles): Miller-columns file manager with instant contextual previews.
  - [**`miqumusic`**](https://github.com/miqu-project/miqu/tree/main/apps/miqumusic): Fast, lightweight MPD client and audio playback interface.
  - [**`miqugallery`**](https://github.com/miqu-project/miqu/tree/main/apps/miqugallery): Smooth image viewer and media gallery.
  - [**`miqutheme`**](https://github.com/miqu-project/miqu/tree/main/apps/miqutheme): Dynamic wallpaper palette extraction and visual theme manager.
  - [**`miquinfo`**](https://github.com/miqu-project/miqu/tree/main/apps/miquinfo): Real-time hardware telemetry and system resource monitor.

- **Mobile Applications (`mobile/`)**
  - [**`doctor`**](https://github.com/miqu-project/miqu/tree/main/mobile/doctor): Healthcare diagnostic companion app (Android / Jetpack Compose).
  - [**`recitation`**](https://github.com/miqu-project/miqu/tree/main/mobile/recitation): Distraction-free Quran audio recitation and study app (Android / Jetpack Compose).

---

<p align="center">
  <sub>Explore full documentation, screenshots, and specifications at <a href="https://miqu-project.github.io"><b>miqu-project.github.io</b></a>.</sub>
</p>
