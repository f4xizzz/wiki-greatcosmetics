# **Cobblemon Integration**

---

Requires **Cobblemon `1.8.0`** or newer (see [Dependencies](Dependencies.md)). Everything below is either hidden from the UI or silently inert without it.

| Feature | Where | Details |
| :--- | :--- | :--- |
| **Party tab** | `/wardrobe` | Lets a player browse and apply [Pokémon Skins](Pokemon Skins.md) to their party. |
| **Cobblemon Effects popup** | Dev Studio → cosmetic editor → `>> Cobblemon Effects` | Holds everything below. |
| **Lure bonuses** | Cobblemon Effects popup | Shiny odds, guaranteed IVs, EV gain, capture chance, hidden ability, EXP, friendship, wild-spawn type boost, fishing bonuses. See [Cobblemon Effects](Lure System.md). |
| **Scanners** (IVs / Nature / Ability / Size / Dex) | Cobblemon Effects popup | Show extra info above/beside nearby Pokémon while equipped. See [Cobblemon Effects § Scanners](Lure System.md#scanners). |
| **Heal Ability** | Cobblemon Effects popup | Heals the player's whole party, HP/status/PP, on a Shift-hold or a Quick Actions click. See [Special Effects](Attributes.md#special-effects). |
| **Shiny & HA Radar** | Cobblemon Effects popup | Warns the player when a wild shiny/Hidden-Ability Pokémon is nearby. See [Special Effects](Attributes.md#special-effects). |
| **Shiny Effect** | Cobblemon Effects popup | Applies Cobblemon's own shiny particle + sound to the *player*, using the real Cobblemon asset (not a generic particle). |
| **Pokémon Skins** | Party tab / Dev Studio | An entire cosmetic sub-system for reskinning a Pokémon species (see [Pokémon Skins](Pokemon Skins.md)) — the whole feature needs Cobblemon by definition. |

---

## **Without Cobblemon**

* The **Party** tab doesn't appear in the wardrobe.
* The Cobblemon Effects popup (and everything inside it) doesn't appear in the Dev Studio.
* Any Lure/scanner/Heal Ability/Radar/Shiny Effect values already saved on a cosmetic stay in the config file untouched — they just don't do anything until Cobblemon comes back.
* Every other cosmetic feature (models, sounds, attributes, backpacks, armor cosmetics, particle effects, NPC cosmetics, Tags, the wardrobe itself) works exactly the same.
