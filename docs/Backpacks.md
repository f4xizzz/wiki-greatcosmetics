# **Backpacks**

---

A **backpack** is any cosmetic with `isBackpack` enabled. It renders on the player's `BACK` slot like a normal cosmetic **and** works as private item storage.

---

## **Configuring one**

In the [Dev Studio](Dev Studio.md) cosmetic editor, **Backpack** section:

| Field | Meaning |
| :--- | :--- |
| **Is Backpack?** | Turns the storage behaviour on. |
| **Backpack Rows** | Chest rows, `1`–`6` (9 slots each). |
| **Backpack Name** | MiniMessage title shown at the top of the chest GUI. |

Model, slot (`BACK`), attributes and sounds are configured like any other cosmetic — a backpack can also give armor, flight, effects, Lure bonuses, etc.

---

## **Opening it**

* The player must have the backpack cosmetic **equipped**.
* Press the backpack keybind (default **`B`**), or bind it in **Options → Controls → GreatCosmetics**.
* If the player wears **several** backpacks, a small picker appears first.

---

## **Storage & safety**

* Contents are saved to the database **on every change**, not just on close — a crash won't lose items.
* Contents are per-player and per-backpack-cosmetic. Removing the cosmetic from a player does **not** delete the stored items — re-granting it brings them back.

---

## **Sounds**

Set a **Backpack Sound** (with volume / pitch) in the cosmetic's Sounds section to play a sound when the backpack opens.
