# AGENTS.md — Miqu Ecosystem Coding Rules & Workflow Guidelines

This document is the single source of truth for coding standards, anti-AI-slop enforcement, and workflow protocols across all components of the Miqu desktop environment.

**Companion Files:**
- [VISION.md](file:///home/anisur/projects/VISION.md) — Author's vision & strategic goals.
- [ARCHITECTURE.md](file:///home/anisur/projects/ARCHITECTURE.md) — Ecosystem component roles & descriptions.
- [INSTALLATION.md](file:///home/anisur/projects/INSTALLATION.md) — Installation, build guidelines & toolkit dependency order.
- [TODO.md](file:///home/anisur/projects/TODO.md) — Active roadmap and upcoming tasks.
- [AUDIT_RULES.md](file:///home/anisur/projects/AUDIT_RULES.md) — Ecosystem audit matrix, quality standards, and component compliance status.
---

## Code Writing Rules & Craftsmanship Standards

### Strict Layer Boundaries
1. **Never bypass the toolkit in downstream apps**: Downstream applications (e.g. `miqumusic`, `miqulauncher`, `miqudesk`) must **not** deal directly with raw Pango, Cairo, or low-level surface protocols when `miqutoolkit` can and should handle it.
2. **Push reusable controls into `miqutoolkit`**: If an application requires a UI widget (e.g., a seekbar in `miqumusic`, a dropdown in `miqusecure`), build that widget inside `miqutoolkit` rather than implementing ad-hoc drawing inside the app.
3. **Seek permission before editing `miqutoolkit`**: When working on an application and a toolkit addition or modification is required, always ask the user for permission before modifying `miqutoolkit`.
4. **Full-stack evolution**: We are free to modify any layer of the stack—including the compositor `miquland`—if a protocol, hook, or capability is missing.

---

### Code Craftsmanship & Anti-"AI Slop" Standards
AI-generated code often falls into "Minimum Viable Whatever" (satisficing the immediate prompt while accumulating architectural debt). In this ecosystem, the following rules are strictly enforced:

#### 1. Aggressive Modularization (No God Methods or Bloated Classes)
- **Small, Single-Responsibility Functions**: Keep functions focused. If a method exceeds ~40–50 lines or performs multiple distinct phases (e.g. input validation, geometry calculation, scene graph manipulation, and event binding), decompose it into small private helper functions.
- **Focused Classes**: Keep classes dedicated to a single domain. Do not allow manager classes to become catch-all dumping grounds.

#### 2. Beyond "Just Making It Work" (Lifecycle & Failure-Mode Rigor)
- **The Happy Path is only 25% of the work**: Always handle edge cases, disconnections, cancellations, and errors.
- **Pointer & Lifecycle Safety**: Never retain raw pointers to dynamic entities (`View*`, `Workspace*`, surfaces) without handling their sudden destruction (e.g., app crash, `SIGKILL`, dynamic pruning). Always wire up destroy listeners or validity checks.
- **Deterministic Cleanup (Strict RAII)**: Every scene node, buffer, timer, listener, and memory allocation must have a verified destruction path. Dynamic reload/unload (`dlclose`) must cleanly unbind everything without dangling references.

#### 3. Fail-Fast & Zero Silent Swallowing (No Zombie States)
- **Check Return Values & Negative Syscalls**: Never ignore error return codes from system calls, Wayland protocol methods, or toolkit APIs.
- **No Empty Catches or Log-and-Forget**: Never catch an exception or log an error while continuing execution in a corrupted or half-initialized state. If an operation fails, unwind cleanly or fail fast with clear, actionable diagnostics.

#### 4. Strict Scope-Bound RAII for C Types, Cairo/Pango, and File Descriptors
- **Immediate RAII Wrapping**: Wrap all raw C allocations, file descriptors (`int fd`), Cairo contexts/patterns (`cairo_t*`, `cairo_pattern_t*`), and Pango layouts (`PangoLayout*`) in `std::unique_ptr` with custom deleters or dedicated RAII guards immediately upon acquisition.
- **No Manual Early-Exit Cleanup**: Never rely on manual `close(fd)` or `free()` placed at the end of a function that gets bypassed on early error returns.

#### 5. Zero Magic Numbers & Pure Event-Driven Synchronization
- **Configurable Layouts & Themes**: UI dimensions, margins, colors, and paddings must derive dynamically from configuration files, themes, or layout metrics—never hardcode magic integer literals. Shared appearance tokens (colors, fonts, metrics) are always sourced from `miqutoolkit` via `sync_defaults_from_toolkit()` per Rule 17.
- **Expose Tunables in Asset Configs**: Any feature, metric, timeout, or threshold that is a good candidate for user customization must be exposed in `assets/*.conf` with clear explanatory comments, ensuring zero hidden tunable constants. Root confs vs. downstream app template format follow Rule 17's configuration doctrine.
- **No Sleep-Based Synchronization**: Never use `sleep()`, `usleep()`, or arbitrary timer delays to wait for state transitions or mask race conditions. Always use Wayland protocol callbacks, frame callbacks, event listeners, or event-loop idle handlers.

#### 6. Strict DRY (Don't Repeat Yourself) & Zero Copy-Paste Duplication
- If a logic pattern, event dispatch loop, or geometry calculation repeats more than once, immediately extract it into a parameterized helper function.
- Never duplicate 30–50 line blocks across files with only trivial variable substitutions.

#### 7. Signal Safety & Iteration Invariance (Re-entrancy Prevention)
- **Safe Container Iteration**: Never mutate a container (e.g., vector of views, workspaces, or listeners) while iterating over it. Always work on a copy or use deferred removal queues if traversal can trigger event callbacks.
- **Re-entrancy Guards**: Guard state-changing signal emissions against re-entrant calls that could re-trigger the same event handler recursively.

#### 8. Main-Thread / Event-Loop UI Confinement
- **Wayland & UI Thread Safety**: All Wayland protocol interactions, Cairo/Pango surface rendering, and scene-tree mutations must execute strictly on the main thread / Wayland event loop.
- **Worker Thread Communication**: Worker threads (e.g. background monitoring, MPD sockets, async IO) must never touch UI widgets directly. Communicate state back to the main thread via event file descriptors (`eventfd`), pipes, or event-loop idle handlers.

#### 9. Reuse Existing Code First (Search Before Authoring)
- **Never reinvent the wheel**: Before writing a helper, math calculation, geometry converter, or string utility, inspect the existing codebase.
- **Generalize existing helpers**: If an existing function provides 90% of what is needed, extend or generalize it cleanly rather than writing duplicate private variants.

#### 10. Accurate Naming & Renaming Hygiene
- Names must accurately describe what the code does. Avoid vague identifiers (`temp`, `data2`, `helper`, `process`).
- If refactoring alters a method's scope or responsibility, immediately rename the method and update all call sites.

#### 11. Zero Tolerance for Dead or Abandoned Code
- Immediately excise obsolete functions, unused variables, abandoned header declarations, and commented-out code blocks.
- Never leave "zombie code" behind.

#### 12. Battle-Tested Conventions with Unique Identity
- Adopt industry-standard, battle-tested patterns from top-tier tiling window managers (Sway, Hyprland, etc.) while infusing Miqu's unique design language and architectural elegance.

#### 13. Ripple-Effect & Unintended Consequences Analysis (Blast-Radius Awareness)
- **System-Wide Impact Tracing**: Before adding or modifying any code (e.g., altering class interfaces, event hooks, lifecycle semantics, focus policies, or geometry calculations), proactively analyze and trace its potential **ripple effects** across the entire stack.
- **Zero Myopic Fixes**: Never make isolated "band-aid" edits that solve an immediate symptom while breaking distant subsystems or introducing regressions. Explicitly evaluate and prevent unintended side effects (such as breaking downstream layouts, causing event re-entrancy, or leaving dangling listeners).
- **Verify All Invariants & Call Sites**: When modifying shared structures, protocol hooks, or method signatures, inspect all dependent call sites and downstream components to guarantee end-to-end architectural integrity.

#### 14. Opportunistic Refactoring
- If non-conforming or unmodular code is spotted during analysis of an unrelated task, offer to refactor that part.

#### 15. Radical Candor & Intellectual Honesty (Zero Faking or Sycophancy)
- **Learn to Say "I Could Not Find", "Cannot Do", or "Sorry"**: Never fabricate non-existent APIs, hallucinate symbols, or invent broken workarounds. If something cannot be found in the codebase or is technically impossible under current protocol/library constraints, state clearly and plainly: *"I could not find [X]"* or *"This cannot be done because [Y]"*.
- **Upfront Renderer & Protocol Reality Checks**: Never attempt to "hack around" missing low-level capabilities (e.g., attempting surface corner-radius clipping on stock `wlroots` `wlr_scene` which lacks custom fragment shaders or `scenefx`). State the hard requirement upfront (e.g., *"Stock wlroots cannot clip surfaces to rounded corners without custom GLES shader passes or scenefx integration"*).
- **Zero Pseudo-Solutions & Never Fake Certainty**: If a requirement is ambiguous, unfeasible, requires missing renderer features, or risks system instability, state the limitations honestly and propose genuine architectural prerequisites rather than writing non-functional code or satisficing prompts with broken placeholders.

#### 16. Full-Stack Ecosystem Sovereignty & Zero Defensive Fallbacks
- **End-to-End Stack Control**: We design, build, and maintain the entire Miqu desktop ecosystem—from the `miquland` compositor core and `miqutoolkit` library down to every native first-party application (`miqudesk`, `miqumusic`, `miqusecure`, `miqugallery`, `miquinfo`, etc.).
- **No Speculative or Zombie Fallbacks**: Never introduce defensive fallback branches, heuristic guesswork, or redundant fallback mechanisms (e.g., timeout-based force-kills, manual instant unmapping bypasses, or duplicate secondary destruction paths) for protocols, events, or behaviors that we natively control and guarantee across our own stack.
- **Single Authoritative Pipeline**: Design one clean, unambiguous, protocol-driven contract across layers. If an interaction, event hook, or lifecycle capability is missing or deficient, implement it cleanly at its authoritative source layer (`miquland` or `miqutoolkit`) rather than accumulating downstream workarounds and speculative fallbacks.

#### 17. Canonical Configuration Doctrine & Ecosystem Precedence Rules
- **Canonical Architecture**: This rule governs configuration resolution, template structure, and fallback hierarchy across all Miqu components.
- **Three Distinct Architectural Models**:
  1. *`miquland` (Compositor — Survival Seeding)*: Runs `ensure_default_files()` on every startup; root conf (`/usr/share/miquland/miquland.conf`) is in the active settings chain as compositor-critical fallback.
  2. *`miqutoolkit` (Shared Toolkit Layer — Dead End Authority)*: `/usr/share/miqutoolkit/miqutoolkit.conf` is **always loaded** on toolkit init and is the final authoritative dead end for all shared tokens (`icon_theme`, colors, fonts, metrics). No user-level `source =` in shipped templates.
  3. *Downstream Apps (`miqusecure`, `miqumusic`, `miqugallery`, etc. — Optional Overlay)*: Never auto-seed user config on startup. Fully functional from the toolkit chain alone. User conf is purely additive. Shipped `/usr/share/<app>/<app>.conf` is a bootstrap template only (never loaded automatically), generated on demand via `--init-config`.
- **Canonical Downstream `main()` Init Order** (all toolkit-based apps must follow this exact sequence):
  ```cpp
  auto engine = AppEngine::create();          // 1. Initialize toolkit (loads miqutoolkit.conf chain)
  // resolve user config path...
  if (!target_conf.empty()) {
      Config::get()->load_from_file(target_conf); // 2. Overlay user app config (if exists)
  }
  engine->setup_config_watcher();              // 3. Register inotify watches for all loaded files
  ```
- **Zero Src-Code Defaults for Shared Settings**: Every shared appearance token (colors, fonts, metrics, `icon_theme`) must have an authoritative value in a conf file, not in a C++ struct initializer. Apps sync from `Config::get()` via a `sync_defaults_from_toolkit()` pattern — called unconditionally even when no user config exists.
- **Root Conf Completeness**: Both `/usr/share/miqutoolkit/miqutoolkit.conf` and `/usr/share/miquland/miquland.conf` must have **every setting explicitly defined** (never commented out). Any new setting added in code must be added to the root conf before merge.
- **Live Theme Reload Contract**: Apps use `engine->add_theme_change_listener()` to receive toolkit theme changes. The callback must re-sync from `Config::get()` (which the toolkit has already reloaded) and redraw — never call `init_toolkit_defaults()` from downstream apps.
- **Self-Documenting Two-Section Templates**: Every `assets/<app>.conf` template maintains two distinct sections: *Section 1* for explicit app-specific options, and *Section 2* for commented-out toolkit appearance overrides with clear inheritance documentation.

#### 18. Deep Modules with Narrow Interfaces
- Avoid "shallow" abstractions (classes or wrappers with massive public surface areas that do almost nothing, or multiple micro-classes passing data back and forth without real encapsulation).
- Strive for **deep modules**: rich, comprehensive internal functionality concealed behind a minimal, clean, and declarative public API (gray-box design).
- Downstream callers and apps should interact with simple, expressive entry points without having to manage internal state machinery or step through complex multi-stage setup rituals.

#### 19. Interface-First Design (Contract Precedes Implementation)
- Always design and validate public class interfaces, method signatures, data structures, and lifecycle contracts before writing implementation logic.

---

### Workflow & Collaboration Protocols
- **Audit Status Matrix Tracking**: When completing component-level refactors, features, or audits, update the active compliance checkboxes in [AUDIT_RULES.md](file:///home/anisur/projects/AUDIT_RULES.md).
- **Radical Transparency on Blockers & Limits**: Immediately and candidly inform the user whenever an asset, function, or protocol hook is missing or impossible, without guessing or sugarcoating.
- **Ripple-Effect & Regression Disclosure**: When proposing or explaining a non-trivial code change, explicitly state the potential ripple effects, edge cases, and unintended consequences to the user before proceeding.
- **Visual Feedback Verification**: Visual output (colors, margins, animations) cannot always be reliably verified programmatically. Ask the user directly for verification (e.g., *"Is the background showing red as expected?"*).
- **Human Audit & Readability Pass**: For all vibecoded features and non-trivial patches, perform a dedicated cleanup pass to ensure the code is immediately human-readable, cleanly commented, free of cryptic boilerplate, and easily maintainable by human developers before submitting for review.
- **Configuration File Synchronization**: Whenever editing `/assets/*.conf`, ask the user whether to sync changes to `~/.config/*/*.conf` and vice versa.
- **Git Commit & Push**: Always explicitly ask the user before staging, committing, or pushing git changes.

