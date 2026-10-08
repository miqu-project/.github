# ARCHITECTURE.md — Miqu Ecosystem Component Roles

This document defines every component in the Miqu desktop ecosystem and its architectural role.

---

## Component Registry

| Component | Role |
|---|---|
| **`miquland`** | Wayland window manager & compositor (wlroots-based). |
| **`miqutoolkit`** | Application development toolkit & shared UI library (Cairo/Pango/Wayland abstraction). |
| **`miqulauncher`** | Application launcher, dmenu, workspace switcher, and window switcher built with `miqutoolkit`. |
| **`miquoverview`** | GPU-accelerated live workspace expose & overview plugin for `miquland`. |
| **`miqubg`** | Independent wallpaper daemon built with `miqutoolkit`. |
| **`miqudesk`** | Interactive desktop canvas & widget layer built with `miqutoolkit`. |
| **`miqulock`** | Session lock utility (Wayland ext-session-lock). |
| **`miquidle`** | Wayland idle management daemon (ext-idle-notify). |
| **`miqupolkit`** | Polkit authentication agent built with `miqutoolkit`. |
| **`miqusecure`** | Privacy, security, and firewall front-end utility built with `miqutoolkit`. |
| **`miqumusic`** | Lightweight MPD client and music player built with `miqutoolkit`. |
| **`miqugallery`** | Image viewer and media gallery application built with `miqutoolkit`. |
| **`miquinfo`** | System information and hardware monitoring utility built with `miqutoolkit`. |
| **`miqudm`** | Wayland-native Display Manager & greeter with PAM/logind session management built with `miqutoolkit`. |
| **`miqutest`** | Widget testing playground and interactive showcase for `miqutoolkit` components. |
