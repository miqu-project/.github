# TODO.md — Miqu Ecosystem Active & Future Roadmap

This document tracks upcoming tasks, feature roadmaps, and priorities across the Miqu desktop ecosystem.

---

## Active & Future Roadmap

1. **`miquctl` Comprehensive Compositor IPC Utility**: First-party CLI controller communicating with `miquland` over Unix domain socket (workspace switching/querying, window dispatching, monitor configuration, config reload, dynamic plugin management, and runtime diagnostics).
2. **Plugin System v2.0 (After `miquctl`)**:
   - Window & Workspace Event Bus (`on_workspace_switch`, `on_view_map`, `on_view_unmap`, `on_view_focus`, `on_monitor_change`).
   - Touchpad & Touchscreen Multi-Finger Gesture Hooks (3/4-finger swipe begin/update/end, pinch).
   - Per-Plugin Hook Isolation & Dynamic CLI Management (`miquctl plugin list`, `load <path>`, `unload <name>`).
   - Plugin-Defined Configuration Directives (parsed directly from `miquland.conf`).
   - Custom Tiling Layout Engine Registration API (enabling spiral, dwindle, monocle, master-stack plugins).
   - Pre/Post-Render & Frame Tick Hooks.
3. **Next Utilities & Applications**: `miqubar`, `miqushot`, `miqusunset` (gamma control), `miqusettings`, `package manager front end`, `miqupower`.
4. **Configuration Parser & Legacy Alias Deprecation**: Deprecate redundant backward-compatibility wrappers and duplicate syntax in config parser.
5. **Privacy & Security Center (`miqusecure`) Extensions**: OpenSnitch frontend, 1-click Tor enabler, browser privacy advisor, security auditor, LUKS advice, firewall (ufw/nftables) selection, system restore points.
6. **Touch Screen Gestures**: Multi-touch gesture recognition (swipes, pinch-to-zoom, edge gestures) for touchscreen devices.
7. **Virtual Machine Front-End**: Front-end utility to try out Linux distributions.
8. **Firefox Live Preview Fix in `miquoverview`**: Resolve subsurfaces / popup preview bounding in overview cards.
9. **Theming & Transparency Sync**: Theme should update transparency in `miquland.conf` and handle popup/dialog surfaces without global color bleeding.
10. **Floating Window Improvements**: Review move/resize mechanics and config window rules.
11. **Window Border Shading & Gradient Colors (Ecosystem Phase 2 - Client Decorations)**: Extend gradient colors, multi-stop borders, and border shading/elevation to `miqutoolkit` views (`ViewGroup`, `CardView`) and client decorations.
12. **`miqutoolkit` Internal Animation Framework Implementation**: Implement a first-class, frame-driven animation engine natively inside `miqutoolkit` (supporting configurable easing curves, spring dynamics, opacity fades, geometry interpolations, and hover/focus transitions) to provide smooth, high-framerate UI animations across all downstream applications.
13. **`miqubg` Internal Animation & Cross-Fade Transition**: `miqubg` currently relies on `miquland` compositor animations by spawning a temporary second layer surface and tearing it down after a timer. Evaluate and implement native internal animation / cross-fading directly inside `miqubg` and `miqutoolkit` (rendering smooth image transitions inside a single persistent background surface without creating temporary secondary layer surfaces).
14. **Configuration Format Modernization (Lua / Advanced Scriptable Formats)**: Evaluate transitioning or expanding configuration formats across `miquland` and ecosystem components from custom key-value parsers to Lua (e.g. LuaJIT / Sol2) or other expressive configuration formats (enabling programmable rules, dynamic event callbacks, math expressions, and modular config architectures).
