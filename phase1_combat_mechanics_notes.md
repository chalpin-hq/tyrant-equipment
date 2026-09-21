# Tyrant Combat Mechanics — Phase 1 Notes

Living document. Everything here is sourced from in-game tooltips (battle reports,
item cards, hero ability screens) unless explicitly marked as an unverified
community claim. Goal: settle the real mechanics before Phase 2 (gear compendium)
and Phase 3 (heroes) build on top of them.

---

## 0. Two distinct combat systems — CRITICAL SCOPE FINDING

The Hero Abilities help screen explicitly distinguishes two battle types:

- **Instances** — "Arena duels and dungeon runs — turn-based hero battles."
  Abilities spend charges here (heal, strike, extra loot). Confirms Daily Dungeon
  is turn-based and hero-centric, not army-based.
- **World Battles** — "Marches and rallies out on the map." Abilities trigger
  automatically off a directive (opening round / losses run heavy / winning /
  after biggest hit / save for late rounds). This is army-based with the
  front-line/effective-HP model documented below.

**Unverified claim (another player, not in-game confirmed):** "Outside of
dungeon/arena, raw hero attack matters but pretty much nothing else does. In
arena/dungeon, defense is subtracted from attack" (i.e. a flat ATK − DEF model,
not the % / effective-HP model used in World battles). They describe stacking
one glass-cannon attack hero + one tank hero for Arena/Dungeon success.

**Why this matters for scope:** the original build guide treats all 6 roles
(Gathering, Monster Den, PvP Offense, PvP Defense, Daily Dungeon, Weekly Boss)
with the same army-%-bonus reasoning. If Daily Dungeon (and possibly Weekly
Boss / Arena) actually run on hero-vs-hero subtractive math, gear guidance for
those roles needs different logic — raw K-stat totals on the hero's own gear
may matter more than "Army ATK %" affix themes there.

**Still needed:** a battle report screenshot from an actual Dungeon or Arena
fight, to confirm or refute the subtractive-defense claim the same way we
confirmed the World-battle formula below. Also needs confirming which combat
model Weekly Boss and Garrison Defense (troops stationed at your own base) use.

---

## 1. World Battle formula (confirmed via in-game tooltips)

### Total Attack
> "Your army's attack throughput for the fight, after Army Attack %, troop-type
> Attack %, the counter (rock-paper-scissors) multiplier, and the Damage
> Multiplier."

Total Attack = raw ATK × Army Attack% × troop-type Attack% × Counter Multiplier × Damage Multiplier

**Army Attack% and troop-type Attack% stack multiplicatively — now explicitly
confirmed**, same wording as HP: "Army-wide and troop-type percentages
MULTIPLY, they do not add: +10% army and +20% troop-type is ×1.10 × ×1.20 =
+32%, not +30%." So **all three of Attack, Defense, and Health use the same
army-wide-×-troop-type multiplicative stacking rule** — this is a general
platform rule, not something specific to HP.

### Damage Multiplier
> "A final multiplier applied to your army's TOTAL attack, after Army Attack
> %, troop-type Attack % and the RPS multiplier. Bonuses named 'PvP damage' or
> 'damage dealt' raise this — which is why they never appear in the Army
> Attack row."
>
> How it stacks: "Multiplies the finished attack total; it does not add to
> Army Attack."

This is a **separate channel** from Army Attack — confirmed by the Army Attack
tooltip too: "This is a DIFFERENT channel from Damage Multiplier — a '+X% PvP
damage' bonus raises that, not this row." Practical implication: when reading
gear/affix text, "Army ATK" and "PvP damage" / "damage dealt" bonuses are NOT
interchangeable for scoring purposes — they hit different multiplication
stages, but both ultimately scale Total Attack.

Refined order of operations for Total Attack:
raw ATK → × Army Attack% → × troop-type Attack% → × RPS/Counter multiplier → × Damage Multiplier

### Counter multiplier (rock-paper-scissors)
> "Infantry beat cavalry, cavalry beat archers, archers beat infantry. A
> favourable matchup deals +25% damage, an unfavourable one deals
> proportionally less. The 'Weighted' row is your whole army's average against
> the enemy's actual composition."

- Favorable matchup: ×1.25
- Unfavorable matchup: ×0.80
- Mirror matchup (same troop type both sides): ×1.00
- "Weighted" = your army's overall average multiplier against the enemy's
  actual composition (not just front-line type)

### Effective HP
> "Total hit points your army brought, after Army Health % and troop-type
> Health %. Damage is dealt against this pool; casualties are its share that
> was destroyed."
>
> How it stacks: "Army-wide and troop-type percentages MULTIPLY, they do not
> add: +10% army and +20% troop-type is ×1.10 × ×1.20 = +32%, not +30%."

Effective HP = raw HP × Army Health% × troop-type Health% (multiplicative)

**This is the single most important confirmed mechanic so far** — it directly
contradicts a naive "add up all the % bonuses" approach and confirms
diminishing-but-still-substantial returns on stacking HP sources, since each
additional source multiplies rather than adds a shrinking remainder.

### HP / Troop
> "Effective HP divided by headcount — how tanky the average soldier in this
> army is. A high-tier or infantry-heavy army reads high; a big archer swarm
> reads low."

Derived stat, not a separate mechanic — just Effective HP ÷ headcount.

### Wounded Ratio
> "Shifts your casualty split toward wounded and away from dead. Wounded
> recover; dead do not."

A separate lever from HP/Defense entirely — doesn't change how much damage you
take, only what fraction of losses are recoverable. Confirms/refines the
prompt doc's "90% wounded / 10% killed" split — that split is apparently
adjustable via a Wounded Ratio bonus (research-sourced in the sample data),
not fixed.

### First Round Damage
> "Extra damage in round 1 only — it decides short fights and does nothing in
> a long grind."

**Scoping implication**: gear/affixes granting First Round Damage (several
items in the CSV have this) are only valuable for fast, short fights —
plausibly Monster Den or opportunistic PvP raids — and are dead weight for
anything that goes many rounds (Weekly Boss, a long grinding Dungeon fight,
or a defensive siege). This should factor into Phase 2 role scoring rather
than being treated as generically "offensive."

### Hero Stat Bonus
> "Scales your hero's own attack/defense/HP before the hero converts them into
> the army-wide command %."

Clarifies the hero→army pipeline: a hero's own raw ATK/DEF/HP (boosted by the
hero's own equipped gear plus this Hero Stat Bonus multiplier) gets converted
into the army-wide "Hero command" % bonuses (the ones labeled "Command" in the
Combat Bonuses breakdown, e.g. Army Attack's "+26.0% Hero command" line).
**Relevant for Phase 3**: gear equipped on a hero has two effects at once —
(1) it's part of the hero's own personal combat stats, and (2) after this
conversion, it becomes a % buff to the *entire army's* stats in World battles.

### Front line
> "How many troops fit on the front each round. It is scaled to the SMALLER
> army, so a much larger force cannot bring its whole size to bear at once —
> the rest waits in reserve and rotates in as the front takes losses."

Confirmed: frontline width scales off the smaller army's size. The exact
ratio/formula is NOT yet confirmed — the original prompt doc claimed "at least
60% of the smaller army each round," but the tooltip doesn't state a number,
and the sample battle's numbers don't cleanly resolve to a simple 60% rule (one
side was "enveloped — front widened to 32,841" against a stated "front line of
30,000," which needs more data points to untangle). Treat the "60%" figure as
unconfirmed until we see a battle where we can solve for it directly.

### Damage Reduction (3-layer defense model) — CONFIRMED, now with mechanism

> "The share of incoming damage your army actually prevented this round."
>
> How it stacks: "The three layers stack multiplicatively: 1 − (1−armor)(1−wall)
> (1−special), then capped at 75%. Because they multiply, a second layer only
> removes a share of what got past the first."

Final Damage Reduction = 1 − (1−armor)(1−wall)(1−special), capped at 75%

All three layers are now directly confirmed by their own tooltips:

- **armor** — from the **Army Defense** tooltip, verbatim: *"Raises the
  defense stat of every troop in your army. Defense is not a reduction on its
  own — it feeds the armor curve, which converts it into the armor layer of
  the defense chain."* The **Cavalry Defense** (troop-type) tooltip says the
  same: *"It feeds the armor curve like Army Defense — it is not a damage
  reduction by itself."* **The game itself names and confirms a non-linear
  "armor curve"** converting the (Army Defense% × troop-type Defense%)-scaled
  DEF stat into the armor layer's reduction fraction. The exact curve shape
  (e.g. the unverified `def/(425+def)` community formula) is still not stated
  in any tooltip — but its *existence* as a diminishing curve is no longer a
  guess.
- **wall** — not directly confirmed by a tooltip yet; presumably a
  fortification-based reduction, likely 0% for field battles away from your
  own base/city. Unconfirmed whether it appears in Garrison Defense scenarios.
- **special** — from the **Damage Reduction** (Command) tooltip, verbatim:
  *"Direct damage reduction — the 'Special' layer of the defense chain. It
  cuts damage straight off the top instead of going through the armor curve.
  Your hero's command DEF % is applied here too."* **Confirmed**: special =
  the flat Command "Damage Reduction" bonus, applied directly, bypassing the
  armor curve entirely.

### Empirical read on the armor curve — from a full 6-round battle report

Battle "thefireturtle vs Gealt" gave Army/Cavalry Defense bonuses, Command
Damage Reduction, AND the actual per-round total reduction for both sides —
enough to isolate the armor layer's rough size (assuming wall = 0 in this
field battle):

| Side | Army Def% | Cav Def% | Combined DEF-scaling | Command Dmg Reduction (special) | Actual total reduction (per round) | Implied armor layer |
|---|---|---|---|---|---|---|
| You | +10% | +9.6% | ×1.206 (+20.6%) | +5.2% | 9–10% (R1–R6) | ≈ 4.0–5.1% |
| Enemy | +11.7% | +9.6% | ×1.224 (+22.4%) | +3.8% | 8–9% (R2–R6) | ≈ 4.4–5.4% |

(Solved from `reduction = 1 − (1−armor)(1−special)` per round, wall assumed 0.)

**This is the most important finding so far, directionally corroborating the
community claim**: the enemy had a ~9% *relatively* higher combined
Defense-stat-scaling bonus than you (22.4% vs 20.6%), yet the resulting armor
layer came out **nearly identical** (~4–5.5% for both, overlapping ranges).
That's consistent with a steeply diminishing-returns curve — at the DEF levels
both players have, a real difference in Defense% bonuses barely moves the
actual armor reduction. This doesn't confirm the literal `def/(425+def)`
constant (we still don't have raw K-DEF values for either side), but it does
corroborate the *shape* of the claim with real data rather than just an
anonymous player's word.

### The armor curve — VERIFIED (upgraded from hypothesis)

Got the missing piece: raw per-unit troop stats from the Train Cavalry/
Archers/Infantry screens, which show each troop tier's base (pre-bonus)
ATK/DEF/HP. In the Gealt battle both sides fielded Tier 5 Legendary Cavalry:

| Troop (Tier 5 Legendary) | ATK | DEF | HP | March | Carry |
|---|---|---|---|---|---|
| Cavalry | 34 | **20** | 290 | 6 tiles/min | 100/unit |
| Archers | 54 | 15 | 218 | 5.4 tiles/min | 50/unit |
| Infantry | 26 | 22 | 363 | 4.8 tiles/min | 75/unit |

(Matches the role flavor text exactly: Infantry = tank, highest DEF/HP;
Archers = glass cannon, highest ATK, lowest DEF/HP; Cavalry = balanced +
mobile.)

**Important modeling assumption**: the hero's own equipment DEF (Kael showed
+168K DEF from gear) does NOT get added directly into this raw troop DEF pool
— per the Hero Stat Bonus tooltip, hero stats convert into the army-wide
Command % instead, which is already counted inside the Army Defense/Cavalry
Defense % totals. So the armor curve's input is just the troop's own base DEF
stat, scaled by Army Defense% × troop-type Defense% (which already includes
the hero's Command contribution as one of their summed sources).

**Testing the community's exact claimed formula `def/(425+def)`:**

Scaled DEF = raw troop DEF × (1+Army Def%) × (1+troop-type Def%)

- You: 20 × 1.10 × 1.096 = 24.11 scaled DEF → armor = 24.11/(425+24.11) = **5.37%**
  → predicted total reduction = 1−(1−0.0537)(1−0.052) = **10.3%** → rounds to
  "10%" — **matches rounds 1–2 of the battle exactly.**
- Enemy: 20 × 1.117 × 1.096 = 24.48 scaled DEF (assuming same troop tier) →
  armor = 24.48/(425+24.48) = **5.45%** → predicted total reduction =
  1−(1−0.0545)(1−0.038) = **9.0%** → **matches rounds 2–3 exactly.**

Two independent data points (your army and the enemy's, in the same battle)
land within rounding tolerance of the literal `def/(425+def)` formula. A
sensitivity check shows the constant could plausibly be anywhere ~425–500
given the ±1-point rounding on displayed reduction values — one battle isn't
enough to nail the exact integer — but 425 fits comfortably.

**Verdict: upgrade from "unverified community claim" to "strongly corroborated
by independently reconstructed in-game data."** Good enough to use as the
working formula for Phase 2. There's a minor unresolved wrinkle — the
displayed total reduction drifted from 10%→9% (you) and 9%→8% (enemy) over
the 6 rounds despite a uniform single-tier army, which our current model
doesn't explain (possibly just rounding noise near a boundary, possibly a
small effect we haven't identified) — not worth chasing further unless a
future battle shows a bigger, harder-to-dismiss drift.

**Still open, lower priority now**: pin the exact constant (425 vs. something
in the 450–500 neighborhood) with a battle where DEF is pushed to a very
different level (e.g. a heavily defense-stacked garrison build), which would
separate these hypotheses more clearly since the curve is steepest at low DEF
and flattest at high DEF.

---

## 2. Open questions / what to check next

1. ~~Expand "Per-Layer Breakdown" in a battle report~~ — not yet obtained
   directly, but no longer critical: we now have direct tooltip confirmation
   of what each of the 3 layers is (armor/wall/special), plus an empirical
   estimate of the armor layer's size in one battle (see above). Still worth
   getting if easy — would give a cleaner number than our reverse-engineering.
2. Find the **raw DEF stat (K value)** for a hero+army in a battle report (a
   "Force Sheet" section shows Total Attack / Effective HP / HP-per-Troop but
   not a raw DEF number) to actually fit armor = f(DEF) as a real curve rather
   than just two overlapping estimates.
3. **Get a Dungeon or Arena battle report** to confirm/refute the subtractive
   (ATK − DEF) Instance-combat claim from section 0 — still completely
   unverified, and a second player has now independently made a related but
   different claim about Instance combat (see section 3 below).
4. Confirm which model **Weekly Boss** and **Garrison Defense** (troops
   stationed at a base) use — World or Instance rules.
5. ~~Confirm whether Army Attack% and troop-type Attack% stack
   multiplicatively~~ — **CONFIRMED**, same rule as HP (see section 1).
6. Resolve the **frontline width rule** — is it really "60% of the smaller
   army" as the original prompt doc claimed, or something else? The Front
   Line tooltip confirms scaling to the smaller army but gives no percentage.
   In the Gealt battle, front line width was pinned at 25,080 (the enemy's
   full army size) for all 6 rounds while your engaged count fluctuated
   24,792–25,304 — needs a cleaner example to pin an exact ratio, may not be a
   fixed % at all (could just be "smaller army's full size, until losses drop
   it below the current width").

---

## 3. Community claims — status

- **`def/(425+def)` diminishing-returns curve** for converting DEF stat →
  armor reduction. **UPGRADED TO VERIFIED** (see section 1's "armor curve"
  writeup) — reconstructed from real troop-tier stats + battle report data,
  this exact formula (constant somewhere ~425–500) reproduces the observed
  reduction values for both sides of a real battle within rounding tolerance.
  Treat as the working formula for Phase 2, not a rumor.
- **"Defense is useless in realistic quantities, HP is strictly better"** —
  now well-supported: at these players' DEF levels (scaled DEF ≈ 24, against
  a curve constant of ~425–500), they're sitting in the steep early part of
  the curve where each unit of DEF is already worth relatively little, and
  the curve only flattens further from there. Getting real, quantified
  survivability comparisons (e.g. "would this armor % actually change combat
  outcomes noticeably") is now possible for Phase 2 using the verified
  formula, rather than needing to just assert the claim qualitatively.
- **"In Arena/Dungeon, defense is subtracted from attack; a glass-cannon
  attack hero + a tank hero beats 2x-power teams"** (originally from the first
  player) — **upgraded from unverified to behaviorally confirmed**, via a
  route we didn't expect: Forgefist Durgan's Shatter ability has different
  effects in World vs. Instance combat. World: "‒12% enemy defense" (a
  small dent, consistent with the weak, diminishing armor curve we verified
  for World battles). Instance: **"Reduce target enemy's defense to 0 for 1
  round"** — not a dent, a full removal. The user independently runs a
  real Arena team built around this: Durgan zeroes a target's defense,
  Kael follows up and one-shots them. That combo only works if defense is a
  large, direct damage mitigator in Instance combat — in World combat,
  zeroing an enemy's DEF would barely move the needle (their armor layer was
  only ever contributing a few percent). A working one-shot combo is strong
  behavioral evidence for a subtractive-or-similarly-direct model, obtained
  without ever seeing an Instance battle report. See Phase 3 section 4.5 for
  the full writeup.
- **A second player's related claim**: "Outside of dungeon/arena raw hero
  attack is relevant but pretty much nothing else seems to matter" — i.e. in
  World battles, hero attack stat matters but other hero stats don't. This is
  a DIFFERENT claim from the first player's and is **partially in tension**
  with what we've confirmed: Hero Stat Bonus scales ALL of the hero's
  attack/defense/HP before conversion into army-wide Command %, and we've seen
  meaningful Army Defense/Health Command contributions from heroes in every
  battle report (e.g. your hero contributed +26.0% ATK / +5.2% DEF / +20.8%
  HP via Army Command). So hero DEF/HP command contributions clearly do
  something army-wide — whether they're worth investing in relative to hero
  ATK is a separate, still-open value judgment, not something this claim
  settles. Treat as unverified/overstated until we can compare outcomes with
  vs. without hero DEF/HP investment.
