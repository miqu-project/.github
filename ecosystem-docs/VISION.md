# VISION.md — Miqu Ecosystem Vision & Strategic Goals

---

## The Challenge: Competing with Modern Wayland Powerhouses
Our overarching ambition is to challenge and stand alongside elite Linux desktop configurations (such as Omarchy, which pairs Arch Linux with Hyprland and Quickshell). These environments set high benchmarks for performance, fluidity, and modern aesthetics.

However, existing ecosystems have notable gaps and vulnerabilities:
1. **Lack of a Unified, Mature Application Toolkit**: Projects in competing ecosystems frequently suffer from fragmented or immature toolkits (e.g. `hyprtoolkit`), forcing third-party tools into mismatched frameworks with inconsistent rendering and theme behavior.
2. **Abandonment of Native First-Party Applications**: Many modern tiling compositors have stepped back from building cohesive, first-party native desktop applications, creating disjointed user experiences.
3. **Absence of a Native Display Manager**: Greeters and session managers remain third-party afterthoughts rather than first-class ecosystem citizens.

## Miqu's Strategic Edge & Differentiators
1. **A Unified Foundation with `miqutoolkit`**: All first-party applications share a single, rock-solid Wayland/Cairo/Pango abstraction library—delivering seamless animation curves, instant theme propagation, and zero UI fragmentation.
2. **First-Party Native App Suite**: We build a fully integrated suite of native utilities designed to work together out of the box:
   - **`miqudesk`**: An approachable, interactive desktop canvas and widget layer bringing the familiar, intuitive usability of Linux Mint into the bleeding-edge Wayland tiling space for casual and power users alike.
   - **`miqusecure`**: An **outstanding**, class-leading privacy, firewall, and security command center (unifying Tor, OpenSnitch, LUKS management, firewall selection, and privacy auditing into a beautiful native interface).
   - **`miqumusic`**: A lightweight, lightning-fast native MPD client and music player.
   - **`miqugallery`**, **`miquinfo`**, **`miqudm`**, **`miqulock`**, **`miquidle`**, and **`miquoverview`**.
3. **Battle-Tested Compositor & Plugin Architecture**: `miquland` leverages the proven reliability of `wlroots` combined with our own growing, highly-extensible plugin and IPC ecosystem (`miquctl`, dynamic hooks, and custom tiling layout engines).
4. **Native Arch Linux Synergy**: Built from the ground up to thrive on Arch Linux—delivering peak performance, zero bloat, and total user sovereignty.
