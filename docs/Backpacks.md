# **Backpacks**

---

A **backpack** is any cosmetic with `isBackpack` enabled. It renders on the player's `BACK` slot like a normal cosmetic **and** works as private item storage.

---

## **Configuring one**

In the [Dev Studio](Dev Studio.md) cosmetic editor, **Backpack** section:

| Field | Meaning |
| :--- | :--- |
| **Is Backpack?** | Turns the storage behaviour on. |
| **Backpack Rows** | Chest rows per page, `1`–`6` (9 slots each). |
| **Backpack Pages** | How many independent pages. `1` = a single chest, no page arrows. |
| **Backpack Name** | MiniMessage title shown at the top of the chest GUI. |

Model, slot (`BACK`), attributes and sounds are configured like any other cosmetic — a backpack can also give armor, flight, effects, Lure bonuses, etc.

---

## **Opening it**

* The player must have the backpack cosmetic **equipped**.
* Press the backpack keybind (default **`B`**), or bind it in **Options → Controls → GreatCosmetics**.
* If the player wears **several** backpacks, a small picker appears first.

Multi-page backpacks show **`<` / `>`** arrows and a **`Page X/Y`** label attached to the chest; switching pages swaps the contents in place without closing the GUI.

---

## **Storage & safety**

* Contents are saved to the database **on every change**, not just on close — a crash won't lose items.
* Each page is stored separately, so existing single-page backpacks keep their items when you later add pages.
* Contents are per-player and per-backpack-cosmetic. Removing the cosmetic from a player does **not** delete the stored items — re-granting it brings them back.

---

## **Sounds**

Set a **Backpack Sound** (with volume / pitch) in the cosmetic's Sounds section to play a sound when the backpack opens.
