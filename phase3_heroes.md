# Phase 3 — Heroes

Builds on [phase1_combat_mechanics_notes.md](phase1_combat_mechanics_notes.md)
and [phase2_gear_compendium.md](phase2_gear_compendium.md). Source: 11 hero
cards sampled from the in-game roster (Stats/Abilities tabs).

---

## 1. Hero mechanics framework

Every hero has three independent sources of impact, confirmed distinct from
each other:

### Specialty (one per hero)
A single named stat — **Attack Bonus, Defense Bonus, Healing Speed, Gather
Speed, March Speed,** or **Training Speed** — seen so far. This is the hero's
main identity and maps to one Command-channel bonus (e.g. Kael's Attack Bonus
+8.8% is the "Specialty" line item under Army Attack in battle reports).
Boosted by the **Specialization Boost** research (+15% to whatever the
specialty produces).

### Troop Affinity (two troop types per hero)
Every hero lists two of the three troop types (e.g. Kael: Cavalry · Infantry;
Theron: Infantry · Archer). Confirmed from the battle report breakdown: this
is a **single flat % applied uniformly to that troop type's Attack, Defense,
AND Health simultaneously** — Kael's "Troop Affinity +8%" appeared identically
under Cavalry Attack, Cavalry Defense, and Cavalry Health in the same battle
report. **This directly contradicts the claim that hero stats outside their
attack don't matter** — Troop Affinity is a broad, all-three-stats buff
regardless of the hero's Specialty type. Boosted by the **Affinity Training**
research (+20%).

### Abilities (2–4 per hero, charge-limited)
Each ability has **separate, differently-worded effects for Instances vs.
World battles** — not just a reskin, genuinely different numbers/mechanics:

- **Instance effects** are direct, single-target or all-enemy combat actions
  (e.g. Power Strike: "Deal 2.5x auto-attack damage to a single enemy";
  Taunt: "All enemies attack this hero for the rest of the round"; Counter
  Stance: "next enemy attacking Theron takes 75% of their damage reflected
  back"). **Taunt, Counter Stance, and Barkskin have no World-battle
  equivalent at all** — they're Instance-only. This makes sense only if
  Instance battles are genuinely single-hero-targeted duels, not an army
  model — the strongest evidence yet (short of an actual battle report) that
  Instance combat is structurally different from World combat.
- **World effects** apply to your whole army, phrased as either:
  - a **damage burst** ("bonus strike equal to X% of specialist attack") —
    confirms these draw from the **hero's own personal Attack stat** ("their
    total attack" / "specialist attack"), not the army-wide Command %. This
    is a mechanic Phase 2 didn't know about: a hero's raw K-ATK (from
    gear+level) has a *third* channel of impact beyond Hero Stat Bonus →
    Command conversion — it also directly scales these ability bursts.
  - a **temporary troop-type buff/debuff** ("+X% defense for one troop type,"
    "-X% enemy defense for one troop type") — round-limited, stacks on top of
    the passive Command/Affinity bonuses, usually gated behind a
    losses-triggered or opening-round directive.

### Ability firing directives (confirmed exhaustive list)
- **Opening round** — fires round 1, before either side has lost anything.
- **When losses run heavy** — fires once 20% of the troops *you* brought
  have fallen.
- **When winning** — fires once 20% of the *enemy* army has fallen.
- **Save for late rounds** — fires from round 6 onward.
- **After their biggest hit** — fires the round after the enemy lands a blow
  1.4x heavier than their usual, or once 15% of your army has fallen,
  whichever comes first.
- **Never** — held in reserve, never fires in World combat (presumably still
  usable manually in Instances).
- **On a specific round** — fires exactly that round; held if the fight ends
  sooner.

Two abilities sharing a directive only one fires per battle (confirmed in
Phase 1) — worth deliberately offsetting a hero's abilities across different
directives rather than defaulting both to "Opening round."

---

## 2. Hero roster (11 heroes sampled)

| Hero | Specialty | Troop Affinity | Key World abilities | Best-fit role(s) |
|---|---|---|---|---|
| **Bloodreaver Kael** | Attack Bonus | Cavalry · Infantry | Power Strike (opening Cav burst, 20% specialist ATK); Bloodlust (finishing Cav burst scaling to 70% specialist ATK when winning) | PvP Offense, Monster Den (Cavalry-led) |
| **Warlord Marcus** | Attack Bonus | Archer · Infantry | Power Strike (Archer burst); Battle Cry (+12% archer attack, 2 rounds) | PvP Offense, Monster Den (Archer-led) |
| **Ironheart Roderic** | Attack Bonus | Infantry · Cavalry | Power Strike (Infantry burst); Execute (locked, unlocks Lv 30) | PvP Offense (Infantry-led) |
| **Ironwall Theron** | Defense Bonus | Infantry · Archer | Bulwark (+12% infantry DEF, 2 rounds, on heavy losses); Riposte (reflect 50% of enemy's last-2-round damage, after their biggest hit); Taunt/Counter Stance (Instance-only) | PvP Defense / Garrison |
| **Bastion Hadrian** | Defense Bonus | Infantry · Archer | Bulwark; Immovable (+15% infantry DEF + returns 10% of fallen infantry, on heavy losses); Taunt (Instance-only) | PvP Defense / Garrison |
| **Stonewall Borin** | Defense Bonus | Infantry · Archer | Fortify (+15% infantry DEF, 2 rounds, on heavy losses; Instance: doubles own DEF); Bulwark; Taunt (Instance-only) | PvP Defense / Garrison |
| **Moonveil Seraphina** | Healing Speed | Archer · Infantry | Heal (returns 15% of lost archers, on heavy losses); Rejuvenation (returns 18% of lost archers, "pulls back even the gravely wounded") | Garrison support (healer — matches the Phase 2 healer note) |
| **Gatherer Elena** | Gather Speed | Cavalry · Infantry | Battlefield Scavenging (recovers 15% of fallen troops' value + 5% of fallen cavalry, post-fight) | Gathering |
| **Leafsong Aelindra** | Gather Speed | Cavalry · Archer | Requisition (+15% loot/carry on victory + 5% ATK for one troop type); Barkskin (Instance-only, +60% DEF 2 rounds) | Gathering (with light combat capability) |
| **Forgefist Durgan** | Training Speed | Infantry · Cavalry | Shatter (-12% enemy infantry DEF, 1 round, opening round) | Base-building / troop training economy — not combat-role-specific |
| **Swiftarrow Lyris** | March Speed | Archer · Cavalry | Rain of Arrows (3-round sustained volley, bonus damage totaling 100% of specialist ATK) | PvP Offense / Monster Den (sustained-fight variant, Archer-led) |
| **Deadeye Kestrel** | Attack Bonus | Archer · Cavalry | Power Strike (Archer opening burst); Culling Fire (late-round execute-style burst, 50% of specialist ATK — bigger payoff than the usual 20% Power Strike) | PvP Offense / Monster Den (Archer-led, highest single-hero burst potential seen so far) |
| **Battlehorn Cassian** | **Leadership** (new type) | Archer · Infantry | Heal (same text as Seraphina's — healing abilities appear to be shared/generic, not specialty-locked); Inspire (Instance-only, restores 1 charge of another hero's chosen ability); Coordinated Assault (+5% attack *per troop type fielded*, best with all three) | General army support / commander — doesn't fit cleanly into the existing 6 roles (see below) |

**Roster update (2026-09-20):** the real hero roster has 13 heroes, not 11 —
Battlehorn Cassian and Deadeye Kestrel were missing from the original sample.
Both added above. Two new findings from their profiles:

- **"Leadership" is a fourth specialty family** alongside Attack/Defense
  Bonus, Healing Speed, Gather/March/Training Speed — Cassian is the only
  example so far. His kit doesn't map onto any single existing role: Heal
  duplicates Seraphina's ability text (suggesting healing kits aren't
  specialty-locked, any "support-flavored" hero can apparently get one),
  Coordinated Assault explicitly rewards running a **mixed** troop
  composition (all three types) rather than a single-type army like every
  other offense hero implies, and Inspire is a pure utility move (restores
  another hero's ability charge). Best read as a flexible support/commander
  pick for a mixed-composition army, not a role-specific specialist.
- **A hero detail screen can show an account-level research bonus above the
  Specialty section** — both Cassian's and Kestrel's screens showed
  "Vanguard Tactics: Hero Presence Attack +3%," in the same slot where
  earlier heroes showed "Affinity Training +20%" / "Specialization Boost
  +15%" / "Recovery Speed +20%". This is account-wide (from research/
  buildings), not a property of the specific hero — don't read it as
  something that differentiates Cassian or Kestrel from the rest of the
  roster.

---

## 3. What this changes about Phase 2's open questions

**Resolved: "hero attack matters, nothing else does outside dungeon/arena"
(the second player's claim) — looks wrong, or at least overstated.** Troop
Affinity confirmed to buff Attack, Defense, *and* Health uniformly for two
troop types on every hero regardless of their Specialty, and multiple heroes'
signature World abilities are pure defensive buffs (Bulwark, Immovable,
Fortify, Riposte) with no attack component at all. If hero DEF/HP genuinely
did nothing in World battles, these heroes' kits would be nonsensical. Treat
the claim as specifically about *Instance* combat (where it may still be
true, unverified) rather than a general statement about World combat.

**Strengthened: Instance vs. World are mechanically distinct systems.**
Taunt/Counter Stance/Barkskin existing *only* in Instances, with single-
target aggro and personal damage-reflection mechanics that don't map onto an
army model at all, is about as strong a confirmation as we'll get without an
actual Instance battle report.

**New for Phase 2 gear reasoning**: a hero's own raw ATK stat (from gear +
level, the "specialist attack" figure) directly scales certain World ability
bursts (Power Strike, Bloodlust, Rain of Arrows), on top of the already-known
Hero Stat Bonus → Command % pipeline. For an offense-specialty hero running
Power Strike/Bloodlust/Rain of Arrows, stacking raw hero ATK (not just Army
ATK% gear) has a second, direct payoff. This nuances Phase 2's PvP Offense
gear picks: Conqueror's Regalia's PvP ATK% is still likely the strongest lever
(Damage Multiplier channel, section 1 of Phase 2), but a weapon/accessory with
very high flat ATK (e.g. Bloodreaver — 42 ATK base, highest in the whole
132-item set) is worth more for an ability-burst-heavy hero than Phase 2's
pure-affix-matching logic accounted for.

---

## 4. Hero-role assignment, reconciled with Phase 2's gear roles

| Role (from Phase 2) | Recommended hero | Reasoning |
|---|---|---|
| PvP Offense | Kael (Cavalry-led) or Marcus (Archer-led) — match to your army's troop type | Attack Bonus specialty + an ability that scales off specialist ATK; pair with Phase 2's Conqueror's Regalia gear for a compounding ATK stack |
| PvP Defense / Garrison | Theron, Hadrian, or Borin | All three Defense Bonus + Infantry/Archer affinity + a losses-triggered infantry DEF buff; pair with Phase 2's HP-first gear philosophy — the hero's ability kit supplies burst defense, the gear supplies sustained HP |
| Monster Den | Kael/Marcus/Lyris, whichever matches your fielded troop type | Same logic as PvP Offense — Monster Den is confirmed World-battle (Phase 2 section 0), so ability-burst-scaling and Command% both apply normally |
| Gathering | Elena or Aelindra | Gather Speed specialty is the direct match; Aelindra's higher Gather Speed (+13.5% vs Elena's +8.1%, per sampled levels) and Requisition's loot/carry bonus make her the stronger pick if levels are comparable |
| Garrison healer (Phase 2's healer note) | Seraphina | Only Healing Speed specialty hero sampled; matches the Vitality Crown swap-in note from Phase 2 exactly |
| Daily Dungeon / Weekly Boss | Unresolved | Since these roles' underlying combat model is still unverified (Phase 2 sections 2.5–2.6), hero assignment here is a placeholder at best. If they turn out to be Instance-based, Taunt/Counter Stance/Barkskin-style heroes (Theron, Borin, Aelindra) become far more relevant than their World-battle kits suggest, since those are literally the abilities that only work in Instances. |

---

## 4.5 Instance battle structure — first real evidence (2026-09-20)

The user's actual in-game team picks give us the first concrete look at how
Instance battles (Dungeon, Arena) are structured, beyond the "separate
loadout exists" structural clue from Phase 2:

- **Teams are 3 heroes.** Dungeon/Weekly Boss: Kael + Bastion Hadrian + Elena.
  Arena: Kael + Bastion Hadrian + Forgefist Durgan.
- **Taunt is used as a real aggro mechanic, not flavor text.** Hadrian
  (Taunt: "all enemies attack this hero for the rest of the round") is run as
  the dedicated tank in both lineups — confirms Instance battles have
  single-target, redirectable aggro, i.e. a traditional RPG-party structure
  (tank absorbs hits, damage dealer kills, support/utility rounds out the
  team) rather than anything resembling the World-battle army model.
- **Dungeon rooms have their own loot pool, boostable via hero ability.**
  Elena's Scavenge/Quick Loot (Instance-only, "increase room loot bonus") are
  being used specifically to maximize Dungeon/Weekly Boss rewards, not for
  combat. Confirms Dungeon content is room-based with its own scoring/loot
  layer separate from the fight itself.
- **The Arena team's real engine is a debuff-into-burst combo, and it's the
  strongest evidence yet on how Instance damage actually resolves.**
  Durgan's Shatter has two completely different magnitudes depending on
  context: World — "‒12% enemy defense" (a small dent, consistent
  with the weak, diminishing armor curve verified in Phase 1 for World
  battles). Instance — **"Reduce target enemy's defense to 0 for 1
  round."** Not a dent — a full removal. The user runs Durgan
  specifically to zero a target's defense so Kael can one-shot them
  afterward, and it works. That combo is only possible if defense is a
  large, direct mitigator of incoming damage in Instance combat — in
  World combat, zeroing an enemy's armor layer would free up only the few
  percent that layer was ever contributing (see Phase 1's Gealt-battle
  analysis). **This is the first real behavioral confirmation of the
  subtractive-ATK-minus-DEF claim** the first player made at the very start
  of this project, obtained without ever seeing an actual Instance battle
  report.

Still not known: the exact formula (literally `ATK − DEF`, or something
similarly direct but not identical), whether Bloodlust has an Instance-
specific effect at all (only its World text was captured in the original
hero-card screenshot), or how multiple simultaneous taunts would resolve
mechanically (untested now that the Arena team uses only one tank).

## 5. Open items

1. ~~Whether more heroes exist beyond this 11-hero sample~~ —
   **resolved**: 13 total, confirmed via the user's real inventory export
   (section 4.5's roster update). Battlehorn Cassian and Deadeye Kestrel
   added.
2. Execute (Roderic, locked until Lv 30) — unknown effect, may change his
   role fit.
3. How hero stats/abilities resolve in Instance battles — **partially
   resolved**: we now have strong behavioral evidence for a direct/
   subtractive-style DEF model (section 4.5's Shatter finding) and confirmed
   3-hero party structure with real aggro (Taunt). Still don't have the exact
   formula or a real battle report with numbers.
4. Gather Speed and Training Speed specialty scaling/stacking rules (additive
   vs. multiplicative, same open question as Phase 2's economy stats) still
   unverified — low stakes, non-combat.

---

## 6. Role assignment — 16 heroes (2026-10-23)

Three new heroes joined: **Silvertongue Aldric** (`emissary_legendary`,
Legendary, "Support"), **Dawnbringer Valeria** (`champion_legendary`,
Legendary, PvE) and **Goldvein Thorek** (`overseer_epic`, Epic, "Utility").
The game now labels heroes with a category (Support, Utility, ...). Troop
affinity for the three new heroes hasn't been recorded yet.

What their screenshots show:
- **Aldric:** every skill bonus is PvP-only — Army Attack +9%, Army Defense
  +7.2%, Damage Multiplier +7.2% (plus a small Infantry ATK/DEF skill). A PvP
  army buffer.
- **Valeria:** every skill bonus is PvE-only, Daily Dungeon-only or
  Arena-only — Army Attack/Defense/Health (PvE), Damage Multiplier (Dungeon,
  Arena), Hero Attack (Arena). Base DEF only 4.8K against 52.8K ATK, so she
  can't take hits herself.
- **Thorek:** Gather Speed skill +14.4% and Gold Gathering skill +3.6%,
  Building Speed +4.5%. His +9.5% Stone Gathering comes only from gear.

### Gathering: one specialist per resource

Five gatherers. Each sticks to one resource, and the recommender now has a
profile per resource (`gatherFood`/`gatherWood`/`gatherStone`/`gatherGold`)
that weights that resource's speed as highly as overall Gather Speed and
ignores the other three. That steers single-resource gear to the right hero.

| Resource | Hero | Why |
|---|---|---|
| Gold | Goldvein Thorek | Gold Gathering skill |
| Food | Gatherer Elena | Food specialist |
| Wood | Leafsong Aelindra | Wood specialist |
| Stone | Stonewall Borin | No hero has a stone skill, so the edge has to come from Stone Gathering gear; Borin's defence makes him the safest to leave on a node |
| Flex | Battlehorn Cassian | Covers whichever resource is short; Aldric now covers the support/commander niche |

Forgefist Durgan comes **off** gathering: his Training Speed only works while
he's garrisoned, so every march cost him that passive.

### Full breakdown

Rank = position in the recommender's priority list (higher rank wins a
contested item). Gear-claim order matters most for the bottom half.

| Hero | Lv / Power | Role | Recommender loadouts (rank) |
|---|---|---|---|
| Bloodreaver Kael | 50 / 175K | PvP Offense lead (Cavalry) + Dungeon/WB & Arena DPS | Offense march (1), Offense instanced (18) |
| Deadeye Kestrel | 49 / 155K | PvP Offense (Archer burst) | Offense march (2) |
| Silvertongue Aldric | 39 / 168K | **New** — PvP support / army buffer | Offense march (3) |
| Bastion Hadrian | 50 / 204K | Garrison (sole defender) + Instanced tank | Defence march (4), Defence instanced (19) |
| Moonveil Seraphina | 50 / 121K | Garrison healer (Healing Speed only works garrisoned) | Defence march (5) |
| Ironwall Theron | 48 / 110K | War-reinforcement standby ("Reinforce" set) | Defence march (6) |
| Ironheart Roderic | 39 / 82K | PvP Offense (Infantry) | Offense march (7) |
| Swiftarrow Lyris | 44 / 68K | PvP Offense / Monster Den (Archer) | Offense march (8) |
| Warlord Marcus | 43 / 51K | PvP Offense / Monster Den (Archer) | Offense march (9) |
| Dawnbringer Valeria | 33 / 71K | **New** — PvE: Monster Den lead; Dungeon DPS candidate | PvE march (10) |
| Goldvein Thorek | 31 / 86K | **New** — Gold gathering | Gathering: Gold (11) |
| Gatherer Elena | 50 / 56K | Food gathering + Dungeon/WB loot | Gathering: Food (12), Defence instanced (21) |
| Leafsong Aelindra | 42 / 74K | Wood gathering | Gathering: Wood (13) |
| Stonewall Borin | 38 / 68K | Stone gathering | Gathering: Stone (14), Defence reserve (17) |
| Battlehorn Cassian | 39 / 62K | Flex gathering | Gathering flex (15), Defence reserve (16) |
| Forgefist Durgan | 39 / 86K | Garrison (Training Speed) + Arena Shatter | Defence instanced (20) — no march loadout |

New `pve` profile (Valeria) scores Monster Damage, Army/troop Attack,
Monster Damage Reduction and First Round Damage — the Monster Den stats that
were taken out of the offense/defense profiles on 2026-09-29.

### Open questions — gear possibly tied up for nothing

1. **Six offense marches.** Kael, Kestrel, Aldric, Roderic, Lyris and Marcus
   all hold a full march kit. If you don't actually field all six, the bottom
   ones (Marcus at 51K, Lyris at 68K) are holding up to 12 items that could
   be fed into upgrades instead.
2. **Durgan's march gear.** He still wears 5 march items but no longer has a
   march job. The recommender treats worn gear as his, so those items are
   locked away from everyone else until you take them off him.
3. **Cassian and Borin's Defence reserve kits** (ranks 16–17). These claim
   bench items for a second job. Drop them if neither hero ever actually
   fills in on defence.
4. **Valeria has no gear.** At rank 10 she only gets what the PvP heroes
   leave. Move her up if Monster Den matters more than the lower PvP slots.
5. **Valeria in Dungeon.** Her Instance abilities aren't recorded yet, so
   swapping her in for Kael's Dungeon DPS slot is untested.
6. **Troop affinity** for Aldric, Valeria and Thorek isn't recorded. It
   matters for Aldric and Valeria, whose troop-specific stats are scored. The
   default split is Infantry-led and can be edited per loadout.
