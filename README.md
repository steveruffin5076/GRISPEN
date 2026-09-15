# GRISPEN

> *"The world went gray. The ink ran red."*

A 2D top-down zombie survival browser game built with **Phaser 3** in pure HTML5/JavaScript. Rendered entirely in a hand-drawn ballpoint-pen sketch style — monochrome world with selective crimson blood accents.

---

## Quick Start

You don't need to install anything. Just serve the folder with any static file server:

```bash
# Python 3 (easiest, ships on every Mac/Linux)
cd grispen
python3 -m http.server 8080
# then open http://localhost:8080 in your browser
```

Or simply double-click `index.html` to open it directly in a browser (Phaser is loaded from a CDN).

## Controls

| Key | Action |
|---|---|
| **WASD / Arrows** | Move |
| **Shift** | Sprint (uses stamina) |
| **Mouse** | Aim (red cone shows swing / shot direction) |
| **Left Click (hold)** | Charge attack; release to swing or shoot |
| **E** | Loot crates / rest & craft at the shelter |
| **1 / 2** | Switch weapon (Knife / Bow) |
| **R** | Craft 5 arrows from 1 wood |

## What's in the Prototype

- Top-down hand-drawn pen art style on paper-textured background
- Open 2000×2000 world with trees, rocks, wood stumps, herb bushes, supply crates, animals, and zombies
- Two weapons (melee knife with arc swing, bow with projectile arrows)
- Charge-to-aim cone (longer hold = more damage + tighter aim)
- Survival stats: Health, Hunger, Stamina — starvation kills you
- Resource gathering (wood, herbs) with respawning nodes
- Loot crates with random drops
- Shelter zone (center) that auto-heals you, cooks meat, makes medicine, and rests you
- Zombie AI that chases and bites; difficulty increases each day (60s = 1 day)
- Small animal AI that wanders and flees; hunting them yields meat
- Minimap, inventory HUD, day counter, kill counter
- Particle effects: blood splatter, chop sparks, damage floaters, slash arcs, screen shake, damage flash

## Project Structure

```
grispen/
├── index.html            — complete single-file game (open this in your browser)
├── GAME_DESIGN_DOC.md    — GDD with mechanics, art direction, roadmap
├── ART_PROMPTS.md        — AI art prompts for generating more sprites/UI/key art
├── README.md             — this file
└── assets/               — AI-generated style-reference images
    ├── logo.png
    ├── player.png
    ├── zombie.png
    ├── animal.png
    ├── tree.png
    ├── rock.png
    ├── stump.png
    ├── bush.png
    ├── crate.png
    ├── shelter.png
    └── ground.png
```

## Deploying

Upload the entire `grispen/` folder to any static host — GitHub Pages, Itch.io (HTML5 upload), Netlify, Vercel, Amazon S3, or even just drop it on any web server. No build step, no dependencies to install.

## Tech

- **Engine:** Phaser 3.70 (loaded from jsDelivr CDN)
- **Language:** Vanilla JavaScript (ES6+), single file, no build tools
- **Physics:** Phaser Arcade Physics (top-down, no gravity)
- **Art:** All gameplay sprites drawn at runtime via Phaser Graphics API (lines, circles, ellipses). The `assets/` folder contains AI-generated reference images for future polished replacement.

## Name

**GRISPEN** is an original, trademark-free name (verified — no existing games). It fuses:
- *gris* (French for "gray") → the monochrome art style
- *pen* → the ballpoint-pen aesthetic
- *grippen* (Germanic "to grip/seize") → the plague's grip on the world

The in-universe plague is called **the Grispen** or **the Grispen Blight**.

## License & Credits

- Game code: built as a prototype for personal/learning use.
- Primary gameplay/art inspiration: *Ares Virus* by Qcplay/Qingci Games (2018).
- Phaser 3 is © Photon Storm Ltd, used under the MIT License.
