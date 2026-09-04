# **Sounds**

---

Every cosmetic can play sounds tied to player actions while it's equipped. Configure them in the [Dev Studio](Dev Studio.md) cosmetic editor, **Sounds** section.

---

## **Sound slots**

| Field | Plays when… |
| :--- | :--- |
| **Equip Sound** | The cosmetic is equipped. |
| **Unequip Sound** | The cosmetic is removed. |
| **Idle Sound** | The player stands still (occasional random trigger after ~2 s idle). |
| **Walk Sound** | The player is moving on the ground. |
| **Fly Sound** | The player is flying. |
| **Shift Sound** | The player starts sneaking. |
| **Backpack Sound** | A backpack cosmetic's chest GUI opens. |

Each has its own **Volume** and **Pitch** (default `1.0`).

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

There is also a server-wide sound preset file at `config/greatcosmetics/sounds.json` used by a few internal actions (e.g. the "you hit a limit" error sound, the equip confirmation). Keys map a short name to `{ id, volume, pitch }`. Edit it and `/gc reload` to change those global feedback sounds.
