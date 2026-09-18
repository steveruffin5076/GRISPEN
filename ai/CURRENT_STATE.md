# CURRENT STATE & LIVE TASK TRACKER

> **Active Milestone:** `v0.2 — Short-Term Roadmap (post-prototype)`
> **Last Updated:** 2026-09-18
> **Build Status:** `PASSING` (single-file `index.html`, no build step; verified with `node --check` on the inline script + headless-browser boot test)
> **Maintained By:** Claude Code

---

## 0. Correction Notice

Earlier versions of this file (and of `PROJECT.md`, `ARCHITECTURE.md`, `CODING_RULES.md`, `FEATURES.md`,
`MILESTONES.md`, `PRODUCT_REQUIREMENTS.md`, `DECISIONS.md`) described a **grid-based tactics RPG**
(Final Fantasy Tactics-style, `src/core/Main.ts`, CT turn queue, height-advantage combat). That project
was never built. The actual, already-built game is **GRISPEN**, a top-down zombie survival browser game
(Phaser 3, single `index.html`, ballpoint-pen art style) — see `GAME_DESIGN_DOC.md` and `README.md` for
the real design authority. Those other `/ai/*.md` files still describe the unrelated tactics RPG and
should not be used to plan tasks until someone rewrites them; go by `GAME_DESIGN_DOC.md` + `index.html`
instead.

---

## 1. Milestone Status Summary

The GDD's own "Prototype Scope" (§9) and "Roadmap" (§10) checklists were also stale: several roadmap
items were already implemented in code (spiders/vomiters/exploders, mobile virtual-joystick controls,
synthesized SFX, localStorage save/continue). Actual state as verified by reading `index.html` directly:

- **Done:** player movement/sprint, charge-to-aim melee (knife) + ranged (bow), zombie/spider/vomiter/exploder
  AI with poison/acid/explosion mechanics, animal wander/flee AI, wood/herb gathering with respawn, loot
  crates, shelter auto-heal + cook/craft-medicine, arrow crafting, day/night difficulty scaling, minimap,
  full HUD, start/pause/game-over screens, mobile touch controls, synthesized WebAudio SFX, localStorage
  save + continue, global error catcher.
- **Just added:** Bodden (the NPC who rescued Neil, per the GDD's story section) now stands at the shelter
  and speaks — a one-time introduction on first arrival, then rotating short flavor lines on later visits.
  This is the first slice of the GDD §10 "NPCs with dialogue" roadmap item.
- **Active Blockers:** None.
- **Pending Assets:** None required — art is 100% procedural (Phaser Graphics API), per GDD §8.

---

## 2. Active Implementation Task Cards

### [x] TASK-V02-01: Bodden NPC with dialogue at the shelter
- **What was built:** `drawBodden()` renders a stationary old-man figure (cane, grey hair, muted robe)
  beside the shelter door. On the rising edge of entering the shelter radius, the scene shows one of
  `BODDEN_LINES` via the existing toast (`msg()`) — index 0 (an introduction) the first time ever, then
  a rotating cycle of short survival/story flavor lines on each later entry.
- **Files touched:** `index.html` (BODDEN_LINES table, `drawBodden`, state flags `wasInShelter` /
  `metBodden` / `boddenLine`, rising-edge trigger in `_update`).
- **Verified:** `node --check` on the extracted inline script; headless Chromium boot (start screen →
  `BEGIN SURVIVAL` → scene creates, HUD/minimap live, Bodden renders at the correct position);
  directly exercised the shelter-enter/leave/re-enter transition (via a temporary, since-removed debug
  hook) to confirm the intro line fires once and later visits rotate through flavor lines with no
  console errors. (Headless Chromium in this sandbox doesn't deliver synthetic keydown events to
  Phaser's KeyboardManager — a pre-existing environment quirk unrelated to this change — so movement
  was driven directly rather than via simulated WASD.)

---

### [ ] TASK-V02-02: Moral choice system (orange/blue dialogue prompts)
- **Priority:** Medium
- **What to build:** GDD §10 roadmap item — branching dialogue choices (kind vs. self-interested) that
  play into the "should we still be kind, or survive" theme. Natural next step once more NPCs exist.
- **Dependencies:** TASK-V02-01 (done) establishes the dialogue/toast pattern to extend.

### [ ] TASK-V02-03: Boss — The Butcher (gas station)
- **Priority:** Medium
- **What to build:** A unique high-HP enemy with a distinct attack pattern, spawned once a multi-zone
  map or a scripted encounter exists. Currently blocked on there being only one zone (the woods).

### [ ] TASK-V02-04: Old Hunter NPC + hidden caches
- **Priority:** Low
- **What to build:** Second NPC per GDD §2 locations table, reusing the Bodden dialogue pattern.

---

## 3. Next Recommended Implementation Task
👉 **TASK-V02-02: Moral choice system**, or, if a second zone is wanted first, **TASK-V02-04: Old Hunter NPC** (smaller, reuses the pattern just built).

---

## 4. Completed Work Archive

- Full prototype (movement, combat, survival stats, crafting, day cycle, all four enemy types, mobile
  controls, SFX, save/continue, pen-sketch art) — see GDD §9. Built prior to this session
  (`d65199c Full GDD rebuild: complete zombie survival game (offline)`).
- TASK-V02-01: Bodden NPC with dialogue — this session.
