# Phase 2 — Gear Compendium & Role Reasoning

Builds on [phase1_combat_mechanics_notes.md](phase1_combat_mechanics_notes.md).
Goal: replace the original prompt doc's build guide (written before any
mechanics were verified) with reasoning that actually follows from what we
now know. Still a reference document, not the tool itself — Phase 3 (heroes)
comes after this.

---

## 0. New structural finding: Dungeon & Arena use a SEPARATE gear loadout

Kael's equipment screen has two tabs: **MARCH** and **DUNGEON & ARENA**. The
game itself lets you equip completely different gear for World battles
(marches/rallies — the "March" loadout) vs. Instance battles (Arena/Dungeon).
This is strong structural confirmation that Instance combat runs on different
enough math that the devs expect different gear — even without a Dungeon/Arena
battle report to verify the exact formula.

**Practical implication**: "Daily Dungeon" gear recommendations in this
compendium are for whatever fills the Dungeon & Arena loadout slot, and their
effectiveness under Instance rules is unverified (see section 2.5). Monster
Den, by contrast, is executed via a March — so it uses the March loadout and
the verified World-battle model applies directly.

---

## 1. The golden rule, given verified mechanics

**For gear specifically, HP-type bonuses beat Defense-type bonuses for
survivability, and content-specific "damage" affixes beat generic Army ATK/DEF
affixes for their matching content.** Two verified facts drive this:

1. **Army/troop-type Defense% feeds the armor curve** (`def/(~425-500+def)`),
   which is steeply diminishing at the DEF levels achievable from gear+hero.
   Army/troop-type **Health%** has no such curve — it's a flat multiplicative
   scale-up of Effective HP, so every point of HP% is worth its full value,
   always. **A gear piece with a Health affix is doing more real work than an
   equal-tier gear piece with a Defense affix.**
2. **Content-flagged "damage" bonuses hit a different, non-diminishing
   channel.** The Damage Multiplier tooltip is explicit: "Bonuses named 'PvP
   damage' or 'damage dealt' raise this [channel] — which is why they never
   appear in the Army Attack row." This channel multiplies the *fully
   computed* attack total (after Army ATK%, troop ATK%, and the RPS
   multiplier), so it stacks with generic Army ATK rather than competing with
   it. The same pattern is a reasonable, though not directly tooltip-confirmed,
   read on "Monster Damage," "Dungeon Damage," and "PvP ATK"/"PvP DEF"
   affixes — they're plausibly all instances of the same "final multiplier for
   this specific content" mechanic. Where an item has one of these
   content-flagged affixes for the role you're building, it's likely
   outperforming a same-rarity item with only generic Army ATK/DEF, not just
   matching it.

**A second golden rule, added after catching an error in the original Monster
Den guide (section 2.2): rarity-driven level caps mean low-rarity "budget"
sets do not actually outperform high-rarity generic gear once the latter is
available.** Item level caps differ by rarity (Common 28, Uncommon 31, Rare
34, Epic 37, Legendary 40 — Phase 1), and only flat ATK/DEF/HP scale with
level; percentage affixes and set bonuses don't. Since those flat stats are
multiplicative factors in the Total Attack / Effective HP formulas, a set
built from Common/Uncommon pieces (like Beastlord's Hunt or Prospector's Kit)
will lose to same-slot Legendary/Epic items on raw stats by likely an order
of magnitude at full investment, which a flat single-digit-percent set bonus
or themed affix cannot offset. Low-rarity themed sets are the right pick
*before* higher-rarity alternatives are available — not after.

**The exact level-scaling formula, reverse-engineered and confirmed (2026-09-21).**
Flat ATK/DEF/HP scale as:

```
stat(level, quality%) = baseStatAtLevel0 × (1 + 0.0634 × level) × (1 + 0.0025 × quality%)
```

Fit from ~20 duplicate items across Common/Rare/Epic in a real inventory export
(R² = 0.998–1.000, growth rate consistent at ~6.3–6.4%/level regardless of
rarity — only the level *cap* differs by rarity, not the per-level rate), then
confirmed against a Legendary item's in-game "show max level" projection
(predicted vs. displayed values within 0.5–1.5%, consistent with K-rounding).
The quality-multiplier range (×1.00 at Q0% to ×1.25 at Q100%) came directly
from the game's own stat panel, not inference. Percentage affixes still don't
scale with level — this formula is flat-stat-only. Practical implication: an
under-leveled higher-rarity item can legitimately outscore an already-maxed
lower-rarity one once you account for its higher ceiling — `tyrant_gear_tool.html`'s
recommender now scores items on this projection rather than current-level
stats for exactly this reason.

One important unverified inference, flagged honestly: **"PvP DEF base%"**
(Warden's Vigil set) is plausibly the defensive mirror of "PvP ATK base%" —
i.e. it may reduce the *attacker's* Damage Multiplier against you, rather than
feeding your armor curve. If true, PvP DEF items are genuinely strong for
defenders in a way Garrison-Defense-labeled items are not. We have no direct
tooltip confirming this (only the attack-side Damage Multiplier tooltip) — the
symmetry is inferred from the identical `+X% PvP [ATK/DEF] base` item text
pattern, not proven. Treat build recommendations that lean on this as
reasoned-but-unverified.

By contrast, **"Garrison Defense X% while stationed"** (Ironoath Signet,
Fortress Shield Helm, Ironwall Boots) is named as "Defense," not "Damage
Reduction" — by the game's own vocabulary split (Army Defense/Cavalry Defense
feed the curve; only the Command "Damage Reduction" stat bypasses it), this
reads as another curve-feeding stat, i.e. **weak**, despite being the
centerpiece of the original PvP Defense build guide.

**No item in the 132-item set carries a flat "Damage Reduction" affix at
all** — that stat appears to be entirely Command/hero/skill-sourced (Phase 3
territory), not itemized on gear. This reinforces that gear's job for
defensive roles is to stack HP (and, if the PvP DEF hypothesis holds, PvP DEF
items), not to chase Defense affixes.

**Troop-type matching**: several items grant a specific troop type's
ATK/DEF/HP (Cavalry/Infantry/Archer) rather than the army-wide version. Since
these multiply with the army-wide bonus rather than replacing it, they're only
valuable if your force actually fields that troop type. Picks below assume a
Cavalry-led force (matching the real battle data we verified against) —
swap for Infantry/Archer-flagged items if your composition differs.

**First Round Damage** (its own tooltip: "does nothing in a long grind") is
scored per-role below based on expected fight length, not treated as
generically offensive.

---

## 2. Role-by-role reasoning and best-in-slot

### 2.1 Gathering — mechanics unchanged, troop-composition note added

Non-combat role — nothing from Phase 1's combat verification changes this
guide much. One addition: Cavalry has both the fastest march (6 tiles/min)
and highest per-unit carry (100/unit) of the three troop types, per the troop
tier data pulled in Phase 1 — a Cavalry-heavy gathering force is structurally
the efficient choice independent of gear.

Two valid builds depending on goals:

| Slot | Min-max pick (if attainable) | Why | F2P-friendly / set-synergy pick |
|---|---|---|---|
| Weapon | King's Musterblade (Legendary) | March Speed + Wood Gathering guar., high raw stats | Harvest Sickle (Rare) — direct Gather Speed guar. |
| Armor | Storewarden Plate (Legendary) | March Speed + Gather Speed guar. | Forager's Cuirass (Uncommon) — +5% Gather Speed base |
| Helm | Sovereign's Diadem (Legendary) | March Speed + Gather Speed guar. | Master Miner's Helm (Epic) — Prospector's Kit piece |
| Boots | Boots of Hermes (Legendary) | +5% March Speed base + Gather Speed guar. | Scoutmaster's Treads (Epic) |
| Ring | Ring of Power (Legendary) | March Speed + Gather Speed guar. | Gold Talisman (Rare) |
| Accessory | Heart of the World (Legendary) | March Speed + Gather Speed guar. | Merchant's Pouch (Uncommon) — Prospector's Kit piece |

The Legendary column has no combat downside to worry about (Gathering doesn't
fight), so it's a strict upgrade over the set pieces *unless* you specifically
want the Prospector's Kit 3pc bonus (Master Miner's Helm + Merchant's Pouch +
Miner's Pick, +6% Gather Speed at 3/3) — in which case run all three set
pieces together rather than mixing one in. **Note**: Gather Speed's own
stacking rule (additive vs. multiplicative across sources) hasn't been
verified — flagged for completeness, low stakes since it's non-combat.

### 2.2 Monster Den — World-battle model applies (fought via March)

**Revised after catching a scale error in the original version of this guide.**
Beastlord's Hunt (Stalker Boots/Wolfhide Vest/Beastfang Dagger/Tracker's Hood)
covers Boots/Armor/Weapon/Helm with "Monster Damage" or "Monster Dmg
Reduction" affixes, and the full 4pc set grants +Army ATK 6%/Army HP 6% in
dens. The original guide treated this as the correct endgame anchor. It isn't
— it's the correct **budget / early-mid-game** anchor, and the distinction
matters:

Item level caps differ by rarity (Phase 1): Common caps at Lv28, Uncommon
Lv31, Rare Lv34, Legendary Lv40. Only the *flat* ATK/DEF/HP numbers scale
with level — percentage affixes (Monster Damage%, the set's own +6% bonus)
don't. Total Attack is `raw ATK × Army ATK% × troop% × Counter × Damage
Multiplier` — raw ATK is a multiplicative factor, not something a flat
percentage bonus can offset. We have direct evidence of how large the
level/quality scaling gap actually is: base CSV weapon ATK values sit around
30–40, but Kael's real endgame Epic gear (Lv37) was contributing hundreds of
thousands of ATK from that same starting point. A Common item stuck 12 levels
below the Legendary cap isn't closing that gap with a +6% set bonus and a
0.9–1.8% Monster Damage affix — those are small next to an order-of-magnitude
raw-stat deficit.

**Two tiers depending on what's actually available to you:**

| Slot | Endgame pick (Legendary/Epic available) | Why | Budget / early-mid-game pick |
|---|---|---|---|
| Weapon | Bloodreaver (Legendary) | ATK 42 — highest raw ATK in the whole item set | Beastfang Dagger (Uncommon) — Monster Damage affix; set piece |
| Armor | Deathless Warplate (Legendary) | Army ATK + Infantry ATK guar., strong raw ATK/DEF/HP at Lv40 cap | Wolfhide Vest (Uncommon) — Monster Dmg Reduction; set piece |
| Helm | Warcrown of Ash (Legendary, ungated) | Army ATK + Archer ATK guar., high raw stats | Tracker's Hood (Common) — Monster Damage base; set piece — SET COMPLETE at 4/4 |
| Boots | Stormcharge Sabatons (Legendary) | Army ATK + Cav ATK guar. + March Speed, high raw stats | Stalker Boots (Rare) — Monster Damage + March Speed; set piece |
| Ring | Ring of the Tyrant (Legendary) | Army ATK + Cav ATK guar., ATK 29, ungated | Glass Cannon Ring (Rare) — Army ATK + First Round Damage |
| Accessory | Heart of Ruin (Legendary) | Army ATK + Archer ATK guar., ATK 27, ungated | Talisman of Slaughter (Rare) — Army ATK |

The set is the right call while you're still working toward Legendary/Epic
gear, or if you're deliberately optimizing for the set-bonus playstyle — not
because it's mathematically superior once higher-rarity alternatives are
actually available. This same level-cap logic likely applies to Prospector's
Kit (Gathering, section 2.1) too — worth revisiting with the same skepticism
if it matters for your progression stage.

### 2.3 PvP Offense — the Damage Multiplier channel is the whole story

Conqueror's Regalia (Fang/Shroud/Cowl/Pendant/Stalkers/Signet) stacks "+X% PvP
ATK base" across up to 6 slots. Per section 1, this hits the Damage
Multiplier channel — a *different, stacking* lever from Army ATK, not a
competing one. Combined with the set's own +0.4%/+0.6%/+1.0% PvP ATK bonus at
2/4/6 pieces, this is a genuinely compounding, non-diminishing stack. **If
attainable this is unambiguously the correct build** — the caveat is it's
gated to "PvP Offense (TH18+, Core only)," so it may be out of reach for a
mid-progress account.

| Slot | Min-max pick | Gating | Ungated alternative |
|---|---|---|---|
| Weapon | Conqueror's Fang (Legendary) | TH18+, Core | Lancebreaker (Rare) — Army ATK |
| Armor | Conqueror's Shroud (Epic) | TH10+ | Vanguard Cuirass (Epic) — Army ATK + Infantry ATK |
| Helm | Conqueror's Cowl (Epic) | TH10+ | Warcrown of Ash (Legendary, ungated) — Army ATK + Archer ATK |
| Boots | Conqueror's Stalkers (Epic) | TH10+ | Nightlunge Boots (Epic) — Army ATK + Cav ATK + March Speed |
| Ring | (no Conqueror ring — Signet is the accessory-tier Legendary) | — | Glass Cannon Ring (Rare) — Army ATK + First Round Damage |
| Accessory | Conqueror's Pendant (Epic) / Conqueror's Signet (Legendary) | TH10+ / TH18+ Core | Voidfang Shard (Epic) — Army ATK + Archer ATK |

First Round Damage is plausibly valuable here too — offensive raids are
attacker-chosen engagements, often short by design, unlike a defender who
must survive whatever length fight is forced on them.

### 2.4 PvP Defense / Garrison — the biggest correction from the original guide

The original guide leaned on Garrison Defense items (Ironoath Signet,
Fortress Shield Helm, Ironwall Boots) as the backbone. Per section 1, those
items' "Defense while stationed" affix most likely feeds the same weak armor
curve as Army Defense — **not** the strong, non-diminishing route. HP and
(if the inference holds) PvP DEF-channel items are the better-justified picks.

| Slot | Pick | Why |
|---|---|---|
| Weapon | Warden's Wardsword (Epic) | +1% PvP DEF base (Damage-Multiplier-analog, unverified but best-reasoned pick); set piece |
| Armor | Warden's Aegis (Legendary, TH18+ Core) / Juggernaut Plate (Legendary, ungated) | Aegis: +2% PvP DEF base, set piece. Juggernaut Plate: HP110K, highest-HP armor in the set, if Aegis is gated out of reach |
| Helm | Warden's Greathelm (Legendary, TH18+ Core) | +2% PvP DEF base; set piece. **Not** Fortress Shield Helm — that's a Garrison Defense (armor-curve) item |
| Boots | Warden's Greaves (Epic) | +1% PvP DEF base; set piece |
| Ring | Sigil of Sanctuary (Epic) | Army Def + Cav Def — acceptable filler since no PvP-DEF ring exists in the set; or prioritize a pure-HP option if one is more available |
| Accessory | Heart of the Mountain (Legendary, ungated) | Highest flat HP (92K) among defense-themed accessories — HP over Defense per the golden rule |

**Healer note carried over from the original guide, still valid**: if
garrisoning a healing hero, Vitality Crown (Rare, +126K HP, Healing Speed
affix) is worth swapping in over a set-piece helm — pure HP plus a
healing-speed affix that amplifies a support hero's specialty is a reasonable
trade against losing the Warden's Vigil helm slot's PvP DEF%.

**If the PvP DEF hypothesis turns out wrong** (i.e. it also just feeds the
armor curve like everything else "Defense"-named), the correct build
collapses to "stack the highest raw HP available in every slot, ignore
Defense affixes entirely." Worth keeping in mind as the fallback interpretation.

### 2.5 Daily Dungeon — unverified combat model, gear picks are provisional

Per section 0, Dungeon uses a separate gear loadout from March combat, and we
have no battle report to confirm how DEF/ATK/HP actually resolve there. Two
scenarios, both plausible:

- **If Instance combat uses flat subtractive math** (per the second player's
  unverified claim — hero ATK minus hero DEF, roughly), then Army-wide %
  affixes on Dungeon gear may do little or nothing, and what matters is the
  hero's own raw K-stats (the numbers shown on the hero equipment screen,
  e.g. Kael's +344K ATK / +168K DEF / +943K HP) — meaning total item *level
  and rarity* (which scale those K-numbers) matters more than which specific
  affix an item has.
- **If Instance combat still uses army-wide-style % scaling** just in a
  turn-based wrapper, then the existing "Dungeon Damage" affixed items
  (Shadow of the Crypt set: Shadowsteel Blade, Wraith Helm, Crypt Warden's
  Plate, Phantom Greaves) are well-justified via the same content-specific-
  channel logic as Monster Damage/PvP ATK.

Given the uncertainty, the safest provisional pick is the full Shadow of the
Crypt set (it's explicitly Dungeon-flagged either way, and even under the
subtractive-math scenario its raw K-stats are competitive for its rarity), while
flagging that this is the least-verified role in the compendium:

| Slot | Pick | Why (provisional) |
|---|---|---|
| Weapon | Shadowsteel Blade (Rare) | Dungeon Damage affix; set piece; SET COMPLETE at 4/4 |
| Armor | Crypt Warden's Plate (Epic) | Army Def + Dungeon Dmg Reduction; set piece |
| Helm | Wraith Helm (Rare) | Dungeon Damage affix; set piece |
| Boots | Phantom Greaves (Epic) | +10% March Speed base + Dungeon Dmg Reduction; set piece |
| Ring | Signet Ring (Rare) | Gather Speed guar. + random slot (roll Dungeon Dmg Reduction if possible) |
| Accessory | Gold Talisman (Rare) | Filler — no Dungeon-flagged accessory exists in the current item set |

**Do not treat this role's guidance with the same confidence as 2.2–2.4.**

### 2.6 Weekly Boss — combat model also unconfirmed

Same uncertainty as Dungeon, compounded: we don't even know if Weekly Boss is
fought via March (World rules, like Monster Den) or as its own Instance-style
raid. The available gear (Titanbreaker set: Titan Cleaver, Dragonscale Armor,
World Ender's Crown, Earthshaker Boots) is itself Dungeon-Damage-affixed,
suggesting the devs link Weekly Boss mechanically to Dungeon rather than to
Monster Den/World combat — treat as leaning Instance-like until proven
otherwise.

| Slot | Pick | Why (provisional) |
|---|---|---|
| Weapon | Titan Cleaver (Legendary) | Army ATK + Dungeon Damage; set piece |
| Armor | Dragonscale Armor (Legendary) | Army Def + Dungeon Dmg Reduction; set piece |
| Helm | World Ender's Crown (Epic) | Army ATK + Dungeon Damage; set piece |
| Boots | Earthshaker Boots (Epic) | +12% March Speed base + Army ATK + Dungeon Damage; set piece |
| Ring | Ironoath Signet (Epic) | Best available generic stats; no Boss-flagged ring exists |
| Accessory | Gold Talisman (Rare) | Filler |

---

## 3. Proposed revision to the role-scoring rubric (for the eventual "Build Your Own" tool)

The original 0–3 point affix-scoring system (Phase 0 prompt doc) predates all
of this verification. Recommended adjustments before it's implemented:

| Affix category | Original implicit score | Revised score | Why |
|---|---|---|---|
| Army/troop Health% | ~2 (grouped with generic defense theme) | **3** | Confirmed non-diminishing; best defensive lever from gear |
| Content-specific damage affix (Monster/Dungeon/PvP ATK) matching the role | 2–3 | **3** | Likely a distinct non-diminishing channel, stacks with Army ATK |
| Generic Army/troop ATK | 2–3 | **2** | Still good, but no longer "as good as" content-specific damage |
| Army/troop Defense, Garrison Defense | 2–2.5 | **1** | Confirmed to feed a steeply diminishing curve at realistic DEF levels |
| PvP DEF base% | not distinguished from Garrison Defense | **2.5 (flagged uncertain)** | Possibly a non-diminishing channel like PvP ATK — unverified, scored cautiously below content-damage's confirmed 3 |
| First Round Damage | flat 1–2 regardless of role | **2 for short-fight roles (Monster Den, PvP Offense), 0 for long-grind roles (Weekly Boss, sustained Dungeon)** | Tooltip explicitly states it "does nothing in a long grind" |
| Wounded Ratio | not scored | **0.5–1, situational** | Doesn't affect survivability, only recoverability |

Not implementing this in code yet — flagging it here so Phase 3 (or a later
tool-build phase) doesn't quietly re-use the old, now-outdated weights.

---

## 4. Open items carried into Phase 3

1. Whether hero DEF/HP command contributions are actually worth investing in
   relative to hero ATK (the second player's claim vs. what we've confirmed
   about the Hero Stat Bonus → Command % pipeline) — this is fundamentally a
   hero-itemization question, belongs in Phase 3.
2. The PvP DEF / Damage-Multiplier-analog hypothesis (section 1) is load-
   bearing for the PvP Defense build guide and still unverified.
3. Dungeon and Weekly Boss combat models remain unconfirmed — Phase 3's hero
   discussion may surface more evidence (e.g. if hero specialty/skill text
   references "Instance" mechanics more explicitly than what we've seen so
   far).
4. The exact armor curve constant (425 vs. up to ~500) is still a range, not
   a pinned integer — low priority, doesn't change any build recommendation
   above since the qualitative conclusion (defense is weak) holds across that
   whole range.
