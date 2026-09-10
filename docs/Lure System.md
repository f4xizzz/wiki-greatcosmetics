# **Cobblemon Cosmetics (Lure + IVs Scanner)**

---

The **Cobblemon Cosmetics** editor lets a cosmetic give **Cobblemon** perks: Lure bonuses (better shiny odds, guaranteed IVs, capture chance, hidden abilities, EXP, friendship, spawn type filter and fishing bonuses) and an **IVs Scanner**.

Configure it in the [Dev Studio](Dev Studio.md) cosmetic editor via **`>> Cobblemon Cosmetics`**. Every field has a hover tooltip. It only does anything with **Cobblemon** installed.

---

## **IVs Scanner**

Turn on **IVs Scanner** on a cosmetic. While a player wears it (or a cosmetic-armor piece with it), the IVs of **every Pokémon within ~48 blocks** — wild included — are shown above its name as a six-line list, one stat per line (`Health`, `Attack`, `Defense`, `Sp. Attack`, `Sp. Defense`, `Speed`), each stat label in its own bold colour.

It is **independent of the Lure `enabled` switch**. Wild Pokémon IVs don't exist on the client, so the server computes and pushes them a few times per second while the scanner is worn.

---

## **How the numbers work**

* **`enabled`** must be on for any of the bonuses to apply.
* Bonuses from **every** equipped Lure cosmetic are **added together** (unlike speed/potion effects, which take the highest).
* "Chance" fields are `0.0`–`1.0` probabilities (`0.25` = 25%). "Multiplier" fields multiply the base amount.
* Shiny and IV rolls happen **on capture**, not on spawn (a deliberate design choice) — so the player must actually catch the Pokémon.
* **Affected Type** is the one exception that touches the **spawn**: it filters which wild species appear around you.

---

## **Cosmetic HUD**

While a player wears any cosmetic that grants something, a HUD appears in the **bottom-left corner** (transparent background) listing **everything** the equipped cosmetics give — grouped as bullets: **Abilities** (flight, backpack, auto-feed), **Attributes** (armor, speed…), **Effects** (potion effects, particle trail), **Lure**, **Fishing**, **Scanner**. Numeric Lure/Fishing bonuses show the **combined** totals the server actually applies. If the list gets tall, it shrinks itself so it never covers more than ~half the screen. Toggle it server-wide with `lureHud` in [Main Config](Main Config.md) (on by default).

---

## **Fields**

| Field | Type | Effect | When |
| :--- | :--- | :--- | :--- |
| **Affected Type** (`lureTYPE`) | text | While active, only species of that type are eligible in **your** wild spawn pool — Cobblemon then spawns normally from what's left, at the normal rate. Other players' spawns are untouched, and your party / NPCs are never affected. If **no** species of that type can spawn in your biome, nothing spawns. Accepts a type name or id (e.g. `fire`). | On spawn |
| **Shiny Multiplier** (`lureShinyMultiplier`) | chance | Chance to re-roll a non-shiny catch into shiny | On capture |
| **Lure IV** (`lureIV`) | count | Number of IVs forced to 31 on the catch | On capture |
| **Per-IV Perfect Chance** (`lureChanceIV`) | chance | Chance, **per IV**, for each of the 6 IVs to roll 31 (independent roll per stat, on top of the ones guaranteed by Lure IV) | On capture |
| **Hidden Ability Multiplier** (`lureHiddenAbilityMultiplier`) | chance | Chance to give the caught Pokémon its hidden ability | On capture |
| **Ultra Rare Multiplier** (`lureUltraRAREMultiplier`) | chance | Chance to upgrade a spawn to the "ultra-rare" bucket | On spawn |
| **Capture Chance** (`lureChanceDeCaptura`) | chance | Chance to turn a **failed** capture into a success | On ball throw |
| **EXP Multiplier** (`lureEXP`) | multiplier | Extra experience for the Pokémon that battled (`0.5` = +50%) | On EXP gain |
| **Exp Share to Party** (`lureExpAllMultiplier`) | on/off | When on, every other **alive** party Pokémon also receives the full XP the active Pokémon gained (EXP Multiplier included). Does **not** apply to candy XP (Rare/Exp Candy). Editor shows this as a toggle. | On EXP gain |
| **Friendship Multiplier** (`lureAmizadeMultiplier`) | multiplier | Extra friendship gained | On friendship update |
| **Fishing Shiny** (`lurePescaShiny`) | chance | Extra shiny chance, fishing only (stacks with Shiny Multiplier) | On fish caught |
| **Fishing IV** (`lurePescaIv`) + **Fishing Per-IV Perfect Chance** (`lurePescaIvChance`) | count + chance | Same as Lure IV / Per-IV Perfect Chance, fishing only | On fish caught |
| **Fishing Speed** (`lurePescaVelocidade`) | value | Adds Cobblemon "Lure" enchant levels to the fishing rod for faster bites | On rod cast |
| **IVs Scanner** (`ivScanner`) | on/off | See the section above — shows every nearby Pokémon's IVs above its name. Independent from `enabled`. | While worn |

---

## **Not implemented yet**

* **EV Multiplier** (`lureEV`) — EV gain is decided inside Cobblemon's battle logic, which exposes no hook.

---

## **Example: a "Shiny Charm" hat**

```json
"lure": {
  "enabled": true,
  "lureShinyMultiplier": 0.05,
  "lureChanceIV": 0.25,
  "lureIV": 2
}
```

Wearing this gives +5% chance to shiny a catch, 2 guaranteed perfect IVs, and a +25% chance for **each** of the other 4 IVs to roll 31. The wardrobe tooltip lists all active bonuses automatically.
