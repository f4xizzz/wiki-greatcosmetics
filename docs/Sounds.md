# **Sounds**

---

Every cosmetic can play sounds tied to player actions while it's equipped. Configure them in the [Dev Studio](Dev Studio.md) cosmetic editor, **Sounds** section.

---

## **Sound slots**

| Field | Plays when… |
| :--- | :--- |
| **Idle Sound** | The player stands still, repeating every **Idle Sound Interval** ticks. |
| **Walk Sound** | The player is moving on the ground, repeating every **Sound Interval** ticks. |
| **Fly Sound** | The player is flying, repeating every **Sound Interval** ticks. |
| **Shift Sound** | The player starts sneaking. |

Each has its own **Volume** and **Pitch** (default `1.0`).

!!! note "Equip / Unequip / Backpack Sound removed"
    These three fields used to exist but were removed from the editor for simplicity — the cosmetic (un)equip and backpack-GUI-open events no longer play any sound.

!!! tip "It travels with the player now"
    Idle, Walk, Fly and Shift sounds are proper entity-tracked sounds, not fixed points in space. They move along with the player as they walk/fly/swim, and any nearby player can hear them — not just the wearer.

---

## **Repeat intervals**

| Field | Meaning |
| :--- | :--- |
| **Sound Interval** | Ticks between repeats of the Walk / Fly sound while that condition holds. Default `8`. |
| **Idle Sound Interval** | Ticks between repeats of the Idle sound while the player stands still. Default `120`, minimum `20`. |

---

## **Sound IDs**

Use any Minecraft or Cobblemon sound event id, e.g.:

* `minecraft:entity.player.levelup`
* `minecraft:block.note_block.pling`
* `cobblemon:gui_click`
* `minecraft:item.armor.equip_leather`

Leave a field **blank** (or `none`) to disable that sound.

---

## **`sounds.json`**

There is also a server-wide sound preset file at `config/GreatCosmetics/sounds.json` used by a few internal actions (e.g. the "you hit a limit" error sound, the equip confirmation). Keys map a short name to `{ id, volume, pitch }`. Edit it and `/gc reload` to change those global feedback sounds.
