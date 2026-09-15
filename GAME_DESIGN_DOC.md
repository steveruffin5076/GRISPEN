# GRISPEN
## Game Design Document (GDD) — Top-Down Zombie Survival Prototype

---

## 1. PROJECT OVERVIEW

**Working Title:** GRISPEN
**Genre:** 2D Top-Down Zombie Survival / Action RPG
**Platform:** Web (HTML5 / JavaScript — browser playable on desktop & mobile)
**Engine:** Phaser 3 (open-source HTML5 game framework)
**Target Audience:** Players aged 13+ who enjoy survival games (Ares Virus, Don't Starve, Project Zomboid, Hotline Miami)
**Core Hook:** A single-file, no-install, no-download browser game rendered in a brooding monochrome "ballpoint pen" sketch aesthetic, with fast twin-stick survival combat, resource gathering, crafting, and moral choices — all playable in one tab.

**Central Question (a.k.a. the game's thematic spine):**
> At the end of the world, should we still be kind and honest — or follow the instinct to survive?

---

## 2. STORY & SETTING

### Setting
A post-apocalyptic world ravaged by the **Ares Virus**, a failed government super-soldier bioweapon that turned most of humanity into mindless "Infectors." Civilization has collapsed. Resources are scarce. Small groups of survivors cling to life, preyed upon both by the infected and by ruthless bandit gangs.

### Protagonist
The player controls **Neil**, an operative of the elite S.O.T. (Special Operations Team). His squad was sent to a sealed research institute to retrieve the only known antibody sample. A traitor within the squad sabotaged the mission, the team was overrun, and Neil was left for dead. Rescued by a mysterious old man named Bodden, Neil must re-arm, rebuild, and press onward through infected territory to finish the mission — if he can survive long enough.

### Locations (Prototype Scope → Full Game)
| Zone | Prototype | Full Game |
|---|---|---|
| **Shelter (Bodden's hut)** | Healing/crafting hub at map center | Fully upgradeable base (workbench, stove, sewing table, chemistry lab) |
| **Surrounding Woods** | Trees, rocks, wood stumps, herb bushes, scattered animals | Hunting grounds, Old Hunter NPC, hidden caches |
| **Randomized Crates** | Loot boxes scattered across map | Placed ruin sites: gas station, village, mine, Locust bandit camp, central city, research institute |
| *(Future)* | — | NPCs with dialogue, moral choices, branching quests, multiple endings (3 endings like Ares Virus) |

---

## 3. CORE GAMEPLAY LOOP

The five pillars of gameplay:

```
SURVIVE → GATHER → CRAFT → FIGHT → EXPLORE → (repeat)
```

1. **Survive** — Manage Health, Hunger, and Stamina meters. Starvation kills. Injuries require medicine. Rest at shelter to recover.
2. **Gather** — Harvest wood stumps, herb bushes, hunt wild animals, loot crates for supplies. Resources respawn over time.
3. **Craft** — At the shelter (or anywhere with simple recipes):
   - 1 Wood → 5 Arrows
   - 2 Herbs → Medicine (heal 30 HP)
   - 1 Meat → Cooked meal (+40 Hunger)
4. **Fight** — Real-time twin-stick combat. Melee (Knife) and ranged (Bow) weapons with a **charge-to-aim cone** mechanic: longer hold = tighter aim + more damage. Enemies have knockback, hit-flashes, HP bars, and AI behavior.
5. **Explore** — 2000×2000 unit open world. Day cycle (60s = 1 day) increases difficulty every day. Minimap reveals your position, zombie positions, and camera viewport.

---

## 4. CONTROLS

| Input | Action |
|---|---|
| **WASD / Arrow Keys** | Move (8-directional) |
| **Shift** | Sprint (consumes Stamina) |
| **Mouse** | Aim (red cone visualizes swing/shot arc) |
| **Left Click** | Hold to charge attack, release to swing/shoot |
| **E** | Interact (loot crates / rest & craft at shelter) |
| **1 / 2** | Switch weapon (Knife / Bow) |
| **R** | Quick-craft arrows (1 wood → 5 arrows) |

---

## 5. GAME MECHANICS IN DETAIL

### 5.1 Player Stats
- **Health (HP):** 0–100. Taking damage (zombie bites, environmental hazards) reduces HP. Reaches 0 = death. Passively regenerates slowly when Hunger > 40% and outside shelter; regenerates fast inside shelter.
- **Hunger:** 0–100. Decays over time (~80 seconds from full to zero). At zero, player loses 3 HP/sec. Cooked meat restores 40.
- **Stamina:** 0–100. Consumed by sprinting (30/sec). Regenerates when idle (24/sec) or walking (12/sec).

### 5.2 Weapons
| Weapon | Type | Damage | Range | Charge Behavior | Ammo |
|---|---|---|---|---|---|
| **Knife** | Melee arc | 15–40 | 55–70 | Wider arc + higher damage when charged | Infinite |
| **Bow** | Ranged projectile | 25–60 | 240–270 | Narrower cone + faster arrows + higher damage | Wooden arrows (crafted, inventory-based) |
| *(Future)* | Pistol, Shotgun, Sniper Rifle, Molotov, Traps, Axes, Spears, Toxic/Flaming/Narcotic arrows |

### 5.3 Enemies
| Enemy | HP | Behavior | Drops |
|---|---|---|---|
| **Infector (Zombie)** | 28–55+ | Chases player within ~500 units, bites at melee range; speed increases daily | Z-Coins (45%), Rotten Meat (35%) |
| **Wild Animal (Critter)** | 16 | Wanders randomly, flees from player when within 100 units | 2 Raw Meat |
| *(Future)* | Spiders (poison DoT), Vomiters (ranged acid), Explosive Zombies, Bandits/Locusts, Bosses (Butcher, Bone Flecher, etc.) |

### 5.4 Resources
| Resource | Source | Use |
|---|---|---|
| **Wood** | Chopping wood stumps (3 hits each; respawn after 25s) | Craft arrows, upgrade workbench |
| **Herbs** | Picking green bushes (2 hits each; respawn) | Craft medicine (+30 HP for 2 herbs) |
| **Raw Meat** | Killing animals / zombie drops | Cook at shelter for +40 Hunger |
| **Arrows** | Crafted (1 wood → 5), found in crates | Bow ammunition |
| **Z-Coins** | Zombie kills, crates | Currency for future NPC merchants |

### 5.5 Day/Night & Difficulty Scaling
- Each in-game day = **60 real seconds**.
- Every day: zombie spawn cap increases (+2), base HP increases (+~9), movement speed increases.
- Message broadcast: "Day N — The infected grow restless..."
- Spawn interval decreases over time (from 5s down to 2s minimum).

### 5.6 Death & Restart
- When HP reaches 0, the game pauses and shows "YOU DIED" with final statistics (days survived, zombie kills).
- "TRY AGAIN" button resets the scene fresh.

---

## 6. ART DIRECTION

### Core Style: "Ballpoint Pen Sketch"
The defining aesthetic is **hand-drawn ballpoint pen art on paper**, in the spirit of Ares Virus's iconic pen-ink look:

- **Color palette:** ~90% monochrome grayscale/sepia on a warm off-white ("paper") background, with highly selective saturated accents:
  - **Crimson red** — blood, danger, health bar, direction marker, attack cone (melee)
  - **Amber/orange** — fire, ranged attack cone, stamina/hunger accents
  - **Muted green** — herbs, foliage, poison
  - **Dark blue** — player indicator
- **Linework:** Visible, slightly imperfect pen strokes; cross-hatching for shadows; stippling for texture. Lines have weight variation like a real ballpoint.
- **Imperfection:** Circles are jittered (not perfect), trees have asymmetrical canopies, textures have small random dots for "paper noise." This avoids sterile vector feel.
- **Perspective:** Strict fixed top-down (bird's-eye/zenithal) view, no rotation, no isometric tilt.
- **Visual hierarchy:** Because the world is desaturated, anything colored (blood, herbs, fire, UI bars) instantly draws the eye — which is both atmospheric *and* a gameplay readability advantage.
- **UI:** Courier/monospace font, dark semi-transparent panels with thin borders, same sketch aesthetic.

### Camera
- Smooth-follow camera (Phaser lerp ~0.12)
- Zoom level: 1.1x for clarity
- World bounds clamped; camera cannot scroll past edges
- Screen shake on damage
- Brief red vignette flash when player is hit

### Effects
- Blood particle splatter on hits (red dots with fade/tween)
- Chop/spark effects on resource harvesting (tiny colored squares popping up)
- Damage floaters (+1 wood / +meat) with upward tween and fade
- Arc slash visual for melee swings
- Hit-flash tint (red) on enemies
- Knockback impulse on struck enemies (recovers over ~10 frames)
- HP bars above enemies (small dark bar + red fill)

---

## 7. USER INTERFACE

### HUD Elements
| Element | Position | Content |
|---|---|---|
| **Status Panel** | Top-left | Health / Hunger / Stamina bars, Day counter, Kill counter |
| **Minimap** | Top-right | 130×130px radar showing player (blue dot), zombies (red dots), shelter (brown square), viewport rectangle |
| **Weapon Panel** | Bottom-left | Equipped weapon, ammo count |
| **Inventory Panel** | Bottom-right | Wood, Herbs, Arrows, Meat, Z-Coins counts |
| **Floating Message** | Top-center | Temporary toast messages ("Found 5 arrows!", "Knife equipped") |
| **Start Screen** | Full overlay | Title, controls, "BEGIN SURVIVAL" button |
| **Game Over Screen** | Full overlay | "YOU DIED", stats, restart button |
| **Error Box** | Center (red) | Visible only if JS throws — shows error + line for debugging |

---

## 8. TECH STACK

- **Engine:** Phaser 3.70 (loaded from CDN — no build tools required)
- **Language:** Vanilla JavaScript (ES6+), single-file, wrapped in IIFE
- **Rendering:** Canvas 2D / WebGL auto-selected by Phaser
- **Physics:** Phaser Arcade Physics (AABB + circular colliders; no gravity — top-down)
- **Styling:** Hand-written CSS for menus/HUD; no frameworks
- **Hosting:** Any static file server (python3 -m http.server during dev; can be deployed to GitHub Pages, Itch.io, Netlify, Vercel, etc.)
- **Assets:** All sprites drawn programmatically at runtime using Phaser Graphics API (lines, circles, rectangles, polygons). No external image dependencies required. Optional AI-generated PNGs included for reference/future replacement.
- **Compatibility:** Desktop (Chrome, Firefox, Safari, Edge), mobile (touch controls would be added later with virtual joysticks)

---

## 9. PROTOTYPE SCOPE (WHAT IS DONE)

- [x] Player movement (8-dir WASD + Shift sprint)
- [x] Mouse aim with charge-attack cone (melee + ranged)
- [x] Two weapons (Knife, Bow + arrows)
- [x] Zombie AI (chase + melee bite)
- [x] Animal AI (wander + flee)
- [x] Resource gathering (wood, herbs) with respawn
- [x] Loot crates
- [x] Shelter zone with auto-heal + crafting
- [x] Crafting system (arrows, healing)
- [x] Survival stats (HP, Hunger, Stamina) with decay/regen
- [x] Day cycle with scaling difficulty
- [x] Pen-sketch art style (monochrome + red accents)
- [x] Particle effects (blood, sparks, floaters, slashes, screen shake, damage flash)
- [x] Minimap
- [x] Inventory HUD
- [x] Start / Game Over screens
- [x] Error handling (global error catcher + red error box)

## 10. ROADMAP (FUTURE FEATURES)

**Short Term (v0.2):**
- [ ] NPCs with dialogue (Old Hunter, Bodden)
- [ ] Moral choice system (orange/blue dialogue prompts)
- [ ] More enemy types (spiders with poison, Vomiters, Explosive Zombies)
- [ ] Boss: The Butcher at the gas station
- [ ] Virtual joystick controls for mobile
- [ ] Sound effects (swing, hit, zombie groan, pickup, ambient wind)

**Mid Term (v0.5):**
- [ ] Multiple zones (forest → village → gas station → suburbs)
- [ ] Blueprints/recipe unlocks
- [ ] Full crafting stations (Sewing Table, Chemistry Lab)
- [ ] Armor system
- [ ] More weapons (Shotgun, Pistol, Molotov, Traps)
- [ ] Special arrows (Toxic, Flaming, Narcotic)
- [ ] Quest log (main quests + side quests + "promises")

**Long Term (v1.0):**
- [ ] Full branching story with 3 endings
- [ ] Locust Organization antagonist arc
- [ ] Save/load system (localStorage)
- [ ] Weather effects (rain, cold temperature mechanics)
- [ ] Music (oppressive ambient score)
- [ ] Polished cutscenes in comic-panel style
- [ ] Itch.io release

---

## 11. CREDITS & INSPIRATION

- **Primary Inspiration:** *Ares Virus* (2018, Qcplay/Qingci Games) — for the ballpoint pen art style, top-down survival combat, and moral-choice storytelling.
- **Tone/Atmosphere references:** The Walking Dead, *Don't Starve* (Klei), *Darkest Dungeon* (Red Hook), Frank Miller's *Sin City* (spot-color technique), *Dead Nation*.
- **Built with:** Phaser 3 framework (https://phaser.io)
