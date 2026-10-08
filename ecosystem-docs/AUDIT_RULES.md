# AUDIT_RULES.md — Miqu Ecosystem Audit Rules & Quality Matrix

This document defines the audit criteria, evaluation protocol, and component compliance status across the Miqu desktop environment. Audits evaluate adherence to the craftsmanship and coding standards established in [AGENTS.md](file:///home/anisur/projects/AGENTS.md).

Periodic ecosystem-wide audits are performed systematically. Audits iterate continuously over time (Audit Phase 1, Audit Phase 2, ..., Audit Phase N), with each audit phase evaluating every component across three standard sub-categories:

---

## Standard Audit Sub-Categories (Evaluated per Phase)

1. **Modularization & Anti-Slop**:
   - Small, single-responsibility functions ($\le 40\text{--}50$ lines).
   - No god methods or bloated classes.
   - Zero dead code, abandoned headers, or commented-out remnants.
   - Descriptive naming hygiene and clean abstractions.
2. **Performance & Lifetime Safety**:
   - Strict RAII and deterministic cleanup for all nodes, buffers, surfaces, and timers.
   - Pointer safety and destroy listener wiring (no dangling references on app crash/pruning).
   - Memory leak profiling, CPU/GPU efficiency, and IPC throughput.
3. **Security & Boundary Enforcement**:
   - Strict layer boundary enforcement (apps never bypass `miqutoolkit` for raw Pango/Cairo rendering).
   - Protocol hardening, sandboxing, and robust input validation.
   - Graceful handling of error paths, unexpected disconnections, and dynamic unloads.

---

## Component Audit Status Matrix (Current: Audit Phase 1)

| Component | Modularization | Performance & Safety | Security & Boundaries | Phase 1 Status | Notes / Last Audit Date |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **`miquland`** | [ ] | [ ] | [ ] | [ ] Passed | Wayland Compositor core |
| **`miqutoolkit`** | [ ] | [ ] | [ ] | [ ] Passed | Core UI Toolkit library |
| **`miqulauncher`** | [ ] | [ ] | [ ] | [ ] Passed | Application Launcher & Switcher |
| **`miquoverview`** | [ ] | [ ] | [ ] | [ ] Passed | Expose / Overview Plugin |
| **`miqubg`** | [ ] | [ ] | [ ] | [ ] Passed | Wallpaper Daemon |
| **`miqudesk`** | [ ] | [ ] | [ ] | [ ] Passed | Desktop Canvas & Widget Layer |
| **`miqulock`** | [ ] | [ ] | [ ] | [ ] Passed | Screen Locker |
| **`miquidle`** | [ ] | [ ] | [ ] | [ ] Passed | Idle Daemon |
| **`miqupolkit`** | [ ] | [ ] | [ ] | [ ] Passed | Polkit Auth Agent |
| **`miqusecure`** | [ ] | [ ] | [ ] | [ ] Passed | Privacy & Security Center |
| **`miqumusic`** | [ ] | [ ] | [ ] | [ ] Passed | MPD Music Player |
| **`miqugallery`** | [ ] | [ ] | [ ] | [ ] Passed | Image & Media Gallery |
| **`miquinfo`** | [ ] | [ ] | [ ] | [ ] Passed | Hardware & System Monitor |
| **`miqudm`** | [ ] | [ ] | [ ] | [ ] Passed | Display Manager & Greeter (Unusable for now) |
| **`miqutest`** | [ ] | [ ] | [ ] | [ ] Passed | Diagnostic & Test Harnesses |

*When an app completes all 3 sub-categories for the active audit phase, mark its Phase Status `[x] Passed` and note the date. When all apps pass, the active cycle advances to the next Audit Phase.*
