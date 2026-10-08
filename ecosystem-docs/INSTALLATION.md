# INSTALLATION.md — Miqu Ecosystem Installation & Build Guidelines

This document defines the strict installation, build restrictions, and dependency sequencing across all Miqu desktop ecosystem components.

---

## 1. Sudo Restriction
- The AI agent **must NEVER execute commands with `sudo`**.

---

## 2. Local Test Builds Only
- For compilation verification and syntax checking during development, always build into the local project `build/` directory without sudo:
  ```bash
  ./make.sh
  ```
- Binaries and shared libraries built locally remain in `build/` strictly for validation.

---

## 3. Strictly System-Wide Installation (`/usr`)
- **NEVER** install, copy, or symlink binaries/libraries into `~/.local/bin` or user home directories.
- All Miqu ecosystem components install system-wide to `/usr` (`/usr/bin`, `/usr/lib`, `/usr/include`) via `sudo ./make.sh`.

---

## 4. Downstream Application Build Dependency Order
- All downstream applications (`miqulauncher`, `miqudesk`, `miqumusic`, `miqugallery`, `miquinfo`, `miqudm`, `miqusecure`, `miqupolkit`, `miqubg`, etc.) dynamically link against the system-wide installed `miqutoolkit` in `/usr`.

### Authoring vs. Building
- You **may** write, edit, and refactor code for downstream applications before updating `miqutoolkit`.
- You **must NEVER** compile or test-build downstream applications until `miqutoolkit` has been rebuilt and installed system-wide.

### Mandatory Step-by-Step Protocol
1. Make edits to `miqutoolkit`.
2. Validate compilation locally (`cd miqutoolkit && ./make.sh`).
3. **STOP immediately**.
4. Prompt the user to install `miqutoolkit` system-wide:
   ```bash
   cd /home/anisur/projects/miqutoolkit && sudo ./make.sh
   ```
5. **Wait for user confirmation** that the system installation has completed before running `./make.sh` on any downstream application.
