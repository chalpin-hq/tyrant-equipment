# Tyrant Gear & Hero Optimization Tool

A single self-contained HTML app for the mobile strategy game **Tyrant** — a gear reference,
build planner, and gear recommender built from verified, reverse-engineered combat mechanics
rather than guesswork.

**Live tool:** https://chalpin-hq.github.io/tyrant-equipment/tyrant_gear_tool.html
*(once GitHub Pages is enabled for this repo — see below)*

## What's in here

- **`tyrant_gear_tool.html`** — the tool itself. No build step, no dependencies; open it directly
  or host it as a static file. Three areas:
  - **Gear Reference** — all reference items, filterable by slot/role.
  - **Build Your Own** — a theoretical loadout builder with set-bonus and role-fitness scoring.
  - **My Roster** — paste or upload your actual in-game inventory CSV export to see your real
    heroes and gear, and run the **Gear Recommender**: a flat, user-editable priority list of
    (hero, job) loadouts that scores items on their *projected max level* (not current level —
    an under-leveled Legendary can legitimately beat an already-maxed Epic once you account for
    its higher ceiling), respects set bonuses, and tracks March vs. Instanced loadouts
    independently per hero.
- **`phase1_combat_mechanics_notes.md`**, **`phase2_gear_compendium.md`**, **`phase3_heroes.md`**
  — the research trail: verified combat formulas (Effective HP, damage reduction, the armor
  curve, the reverse-engineered level-scaling formula), per-role best-in-slot gear, and the
  hero roster with specialties and roles.
- **`tyrant_gear_data.csv`** — the abstract 132-item reference catalog the tool ships with.
- **`tyrant_claude_code_prompt.txt`** — the original build brief.

## Privacy

The My Roster tab runs entirely client-side — pasting or uploading your inventory export never
leaves your browser.

## Enabling GitHub Pages (one-time, manual)

1. Go to **Settings → Pages** on this repo.
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Branch: **main**, folder: **/ (root)**. Save.
4. The tool will be live at the URL above within a minute or two.
