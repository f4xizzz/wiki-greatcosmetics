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

---

## **Lure HUD**

While a player wears one or more Lure cosmetics (or cosmetic-armor) with `enabled: true`, a small column appears to the **right of the hotbar** showing the **combined** bonuses — the same summed totals the server actually applies. It disappears when no Lure is active. Toggle it server-wide with `lureHud` in [Main Config](Main Config.md) (on by default).

---

## **Fields**

| Field | Type | Effect | When |
| :--- | :--- | :--- | :--- |
| **Shiny Multiplier** (`lureShinyMultiplier`) | chance | Chance to re-roll a non-shiny catch into shiny | On capture |
| **Lure IV** (`lureIV`) | count | Number of IVs forced to 31 on the catch | On capture |
| **IV Chance** (`lureChanceIV`) | chance | Chance to apply the guaranteed IVs | On capture |
| **Hidden Ability Multiplier** (`lureHiddenAbilityMultiplier`) | chance | Chance to give the caught Pokémon its hidden ability | On capture |
| **Ultra Rare Multiplier** (`lureUltraRAREMultiplier`) | chance | Chance to upgrade a spawn to the "ultra-rare" bucket | On spawn |
| **Capture Chance** (`lureChanceDeCaptura`) | chance | Chance to turn a **failed** capture into a success | On ball throw |
| **EXP Multiplier** (`lureEXP`) + **Exp All Multiplier** (`lureExpAllMultiplier`) | multiplier | Extra experience gained by the owner's Pokémon (the two values add) | On EXP gain |
| **Friendship Multiplier** (`lureAmizadeMultiplier`) | multiplier | Extra friendship gained | On friendship update |
| **Fishing Shiny** (`lurePescaShiny`) | chance | Extra shiny chance, fishing only (stacks with Shiny Multiplier) | On fish caught |
| **Fishing IV** (`lurePescaIv`) + **Fishing IV Chance** (`lurePescaIvChance`) | count + chance | Extra guaranteed IVs, fishing only | On fish caught |
| **Fishing Speed** (`lurePescaVelocidade`) | value | Adds Cobblemon "Lure" enchant levels to the fishing rod for faster bites | On rod cast |

---

## **Not implemented yet**

These fields exist in the editor but currently do **nothing** — they're reserved for future mechanics:

* **Affected Type** (`lureTYPE`)
* **Fishing Ultra Rare** (`lurePescaUltraRare`)
* **Fishing Lure** (`lureDePesca`)
* **EV Multiplier** (`lureEV`) — EV gain is decided inside Cobblemon's battle logic, which exposes no hook.

---

## **Example: a "Shiny Charm" hat**

```json
"lure": {
  "enabled": true,
  "lureShinyMultiplier": 0.05,
  "lureChanceIV": 0.5,
  "lureIV": 3
}
```

Wearing this gives +5% chance to shiny a catch and a 50% chance for 3 perfect IVs. The wardrobe tooltip lists all active bonuses automatically.
