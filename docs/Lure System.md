# **Lure System**

---

The **Lure** system lets a cosmetic give **Cobblemon** gameplay bonuses: better shiny odds, guaranteed IVs, capture chance, hidden abilities, EXP, friendship and fishing bonuses.

Configure it in the [Dev Studio](Dev Studio.md) cosmetic editor via **`>> Configure LURE`**. It only does anything with **Cobblemon** installed.

---

## **How the numbers work**

* **`enabled`** must be on for any of the bonuses to apply.
* Bonuses from **every** equipped Lure cosmetic are **added together** (unlike speed/potion effects, which take the highest).
* "Chance" fields are `0.0`–`1.0` probabilities (`0.25` = 25%). "Multiplier" fields multiply the base amount.
* Shiny and IV rolls happen **on capture**, not on spawn (a deliberate design choice) — so the player must actually catch the Pokémon.
* **Affected Type** is the one exception that touches the **spawn**: it filters which wild species appear around you.

---

## **Lure HUD**

While a player wears one or more Lure cosmetics (or cosmetic-armor) with `enabled: true`, a small column appears to the **right of the hotbar** showing the **combined** bonuses — the same summed totals the server actually applies. It disappears when no Lure is active. Toggle it server-wide with `lureHud` in [Main Config](Main Config.md) (on by default).

---

## **Fields**

| Field | Type | Effect | When |
| :--- | :--- | :--- | :--- |
| **Affected Type** (`lureTYPE`) | text | Only **wild** Pokémon of that type spawn around you — every other species is blocked. Accepts a type name or id (e.g. `fire`). Only affects your own spawns; never your party or NPCs. If **no** species of that type can spawn in the biome, almost nothing appears. | On spawn |
| **Shiny Multiplier** (`lureShinyMultiplier`) | chance | Chance to re-roll a non-shiny catch into shiny | On capture |
| **Lure IV** (`lureIV`) | count | Number of IVs forced to 31 on the catch | On capture |
| **Per-IV Perfect Chance** (`lureChanceIV`) | chance | Chance, **per IV**, for each of the 6 IVs to roll 31 (independent roll per stat, on top of the ones guaranteed by Lure IV) | On capture |
| **Hidden Ability Multiplier** (`lureHiddenAbilityMultiplier`) | chance | Chance to give the caught Pokémon its hidden ability | On capture |
| **Ultra Rare Multiplier** (`lureUltraRAREMultiplier`) | chance | Chance to upgrade a spawn to the "ultra-rare" bucket | On spawn |
| **Capture Chance** (`lureChanceDeCaptura`) | chance | Chance to turn a **failed** capture into a success | On ball throw |
| **EXP Multiplier** (`lureEXP`) | multiplier | Extra experience for the Pokémon that battled (`0.5` = +50%) | On EXP gain |
| **Exp Share to Party** (`lureExpAllMultiplier`) | fraction (0 = off) | If `> 0`, every other **alive** party Pokémon also receives a fraction of the total XP the active Pokémon gained. `1.0` = full XP to each; `0.5` = half. Already includes the EXP Multiplier. Does **not** apply to candy XP (Rare/Exp Candy). | On EXP gain |
| **Friendship Multiplier** (`lureAmizadeMultiplier`) | multiplier | Extra friendship gained | On friendship update |
| **Fishing Shiny** (`lurePescaShiny`) | chance | Extra shiny chance, fishing only (stacks with Shiny Multiplier) | On fish caught |
| **Fishing IV** (`lurePescaIv`) + **Fishing Per-IV Perfect Chance** (`lurePescaIvChance`) | count + chance | Same as Lure IV / Per-IV Perfect Chance, fishing only | On fish caught |
| **Fishing Speed** (`lurePescaVelocidade`) | value | Adds Cobblemon "Lure" enchant levels to the fishing rod for faster bites | On rod cast |

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
