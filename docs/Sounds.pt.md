# **Sons**

---

Todo cosmético pode tocar sons vinculados a ações do jogador enquanto está equipado. Configure na seção **Sounds** do editor de cosmético do [Dev Studio](Dev Studio.md).

---

## **Slots de som**

| Campo | Toca quando… |
| :--- | :--- |
| **Equip Sound** | O cosmético é equipado. |
| **Unequip Sound** | O cosmético é removido. |
| **Idle Sound** | O jogador fica parado (trigger aleatório ocasional depois de ~2 s parado). |
| **Walk Sound** | O jogador está andando no chão. |
| **Fly Sound** | O jogador está voando. |
| **Shift Sound** | O jogador começa a agachar. |
| **Backpack Sound** | O GUI de baú de um cosmético de mochila abre. |

Cada um tem o seu próprio **Volume** e **Pitch** (padrão `1.0`).

---

## **IDs de som**

Use qualquer id de sound event do Minecraft ou do Cobblemon, ex:

* `minecraft:entity.player.levelup`
* `minecraft:block.note_block.pling`
* `cobblemon:gui_click`
* `minecraft:item.armor.equip_leather`

Deixe um campo **em branco** (ou `none`) pra desativar esse som.

---

## **`sounds.json`**

Também existe um arquivo de presets de som globais do servidor em `config/GreatCosmetics/sounds.json` usado por algumas ações internas (ex: o som de "você bateu num limite", a confirmação de equipar). As chaves mapeiam um nome curto pra `{ id, volume, pitch }`. Edite e `/gc reload` pra mudar esses sons de feedback globais.
