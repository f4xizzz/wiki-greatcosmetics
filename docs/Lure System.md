# **Cobblemon Effects (Lure + Scanners)**

---

The **Cobblemon Effects** editor lets a cosmetic give **Cobblemon** perks: Lure bonuses (better shiny odds, guaranteed IVs, capture chance, hidden abilities, EXP, EV gain, friendship, a wild-spawn type boost and fishing bonuses) and four **Scanners** (IVs, Nature, Ability, Size).

Configure it in the [Dev Studio](Dev Studio.md) cosmetic editor via **`>> Cobblemon Effects`**. Every field has a hover tooltip. The whole page (and the fields below) only appears / does anything on a server that has **Cobblemon** installed.

---

## **Scanners**

Four independent toggles. While a player wears a cosmetic (or an [armor cosmetic](Armor Cosmetics.md)) with any of them on, information about **every Pokémon within ~48 blocks** — wild included — is shown floating near its nametag:

| Scanner | Shows | Where |
| :--- | :--- | :--- |
| **IVs Scanner** (`ivScanner`) | Six lines, one stat per line (`Health`, `Attack`, `Defense`, `Sp. Attack`, `Sp. Defense`, `Speed`), each label in its own bold colour. | Above the nametag. |
| **Nature Scanner** (`natureScanner`) | The Pokémon's nature. | One line above the nametag (below the IV block, if both are on). |
| **Ability Scanner** (`abilityScanner`) | The Pokémon's ability. | To the **right** of the nametag. |
| **Size Scanner** (`sizeScanner`) | Its size category (XS/S/M/L/XL). | To the **left** of the nametag. |

They're all **independent of the Lure `enabled` switch** and of each other — mix and match on the same cosmetic. Wild Pokémon data (IVs, nature, ability, exact size) doesn't exist on the client at all, so the server computes and pushes it a few times per second while any scanner is worn.

---

## **How the numbers work**

* **`enabled`** must be on for any of the *Lure* bonuses (not the Scanners) to apply.
* Bonuses from **every** equipped Lure cosmetic are **added together** (unlike speed/potion effects, which take the highest).
* "Chance" fields are `0.0`–`1.0` probabilities (`0.25` = 25%). "Multiplier" fields multiply the base amount.
* Shiny and IV rolls happen **on capture**, not on spawn (a deliberate design choice) — so the player must actually catch the Pokémon.
* **Affected Type** is the one exception that touches the **spawn** — see below.

---

## **Cosmetic HUD**

While a player wears any cosmetic that grants something, a compact HUD appears in the **bottom-right corner** (transparent background, small text) listing what the equipped cosmetics give — grouped as bullets: **Abilities** (flight, backpack, auto-feed, and any active Scanner), **Effects** (potion effects, particle trail), **Lure**, **Fishing**. Numeric Lure/Fishing bonuses show the **combined** totals the server actually applies. Active scanners are joined on one line, e.g. *"IVs, Nature, Size Scanner"*. If the list gets tall, it shrinks itself so it never covers more than about half the screen. Toggle it server-wide with `lureHud` in [Main Config](Main Config.md) (on by default), or hide it just for yourself from the wardrobe's **Preview** tab.

---

## **Fields**

| Field | Type | Effect | When |
| :--- | :--- | :--- | :--- |
| **Affected Type** (`lureTYPE`) | text | **Boosts** the spawn weight of species of that type in **your** wild spawn pool (species of that type get a large weight multiplier, everything else a small one) — it no longer filters other types out, so spawns keep happening at the normal rate with no "dead air" while it's active. Other players' spawns are untouched, and your party / NPCs are never affected. Accepts a type name or id (e.g. `fire`). | On spawn |
| **Shiny Multiplier** (`lureShinyMultiplier`) | chance | Chance to re-roll a non-shiny catch into shiny | On capture |
| **Lure IV** (`lureIV`) | count | Number of IVs forced to 31 on the catch | On capture |
| **Per-IV Perfect Chance** (`lureChanceIV`) | chance | Chance, **per IV**, for each of the 6 IVs to roll 31 (independent roll per stat, on top of the ones guaranteed by Lure IV) | On capture |
| **Hidden Ability Multiplier** (`lureHiddenAbilityMultiplier`) | chance | Chance to give the caught Pokémon its hidden ability | On capture |
| **Ultra Rare Multiplier** (`lureUltraRAREMultiplier`) | chance | Chance to upgrade a spawn to the "ultra-rare" bucket | On spawn |
| **Capture Chance** (`lureChanceDeCaptura`) | chance | Chance to turn a **failed** capture into a success | On ball throw |
| **EXP Multiplier** (`lureEXP`) | multiplier | Extra experience for the Pokémon that battled (`0.5` = +50%) | On EXP gain |
| **Exp Share to Party** (`lureExpAllMultiplier`) | on/off | When on, every other **alive** party Pokémon also receives the full XP the active Pokémon gained (EXP Multiplier included). Does **not** apply to candy XP (Rare/Exp Candy). Editor shows this as a toggle. | On EXP gain |
| **EV Multiplier** (`lureEV`) | multiplier | Extra EVs gained from battling (`0.5` = +50%) | On EV gain |
| **Friendship Multiplier** (`lureAmizadeMultiplier`) | multiplier | Extra friendship gained | On friendship update |
| **Fishing Shiny** (`lurePescaShiny`) | chance | Extra shiny chance, fishing only (stacks with Shiny Multiplier) | On fish caught |
| **Fishing IV** (`lurePescaIv`) + **Fishing Per-IV Perfect Chance** (`lurePescaIvChance`) | count + chance | Same as Lure IV / Per-IV Perfect Chance, fishing only | On fish caught |
| **Fishing Speed** (`lurePescaVelocidade`) | value | Adds Cobblemon "Lure" enchant levels to the fishing rod for faster bites | On rod cast |
| **IVs / Nature / Ability / Size Scanner** | on/off | See [Scanners](#scanners) above. Independent from `enabled`. | While worn |

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
