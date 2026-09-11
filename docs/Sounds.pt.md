# **Sons**

---

Todo cosmético pode tocar sons vinculados a ações do jogador enquanto está equipado. Configure na seção **Sounds** do editor de cosmético do [Dev Studio](Dev Studio.md).

---

## **Slots de som**

| Campo | Toca quando… |
| :--- | :--- |
| **Idle Sound** | O jogador fica parado, repetindo a cada **Idle Sound Interval** ticks. |
| **Walk Sound** | O jogador está andando no chão, repetindo a cada **Sound Interval** ticks. |
| **Fly Sound** | O jogador está voando, repetindo a cada **Sound Interval** ticks. |
| **Shift Sound** | O jogador começa a agachar. |

Cada um tem o seu próprio **Volume** e **Pitch** (padrão `1.0`).

!!! note "Equip / Unequip / Backpack Sound foram removidos"
    Esses três campos existiam mas foram removidos do editor pra simplificar — os eventos de (des)equipar o cosmético e abrir o GUI da mochila não tocam mais som nenhum.

!!! tip "Agora ele acompanha o jogador"
    Idle, Walk, Fly e Shift Sound agora são sons de verdade amarrados à entidade, não um ponto fixo no espaço. Eles se movem junto com o jogador enquanto anda/voa/nada, e qualquer jogador por perto ouve — não só quem está usando o cosmético.

---

## **Intervalos de repetição**

| Campo | Significado |
| :--- | :--- |
| **Sound Interval** | Ticks entre repetições do som de Walk / Fly enquanto a condição continua valendo. Padrão `8`. |
| **Idle Sound Interval** | Ticks entre repetições do som de Idle enquanto o jogador fica parado. Padrão `120`, mínimo `20`. |

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
