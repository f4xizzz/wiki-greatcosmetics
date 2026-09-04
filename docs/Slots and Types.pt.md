# **Slots & Tipos**

---

O GreatCosmetics limita quantos cosméticos um jogador pode usar com **dois sistemas independentes**: **slots virtuais** (por área do corpo) e **tipos de acessório** (por categoria). Os dois são definidos no [`mainconfig.conf`](Main Config.md) e editáveis no [Dev Studio](Dev Studio.md).

---

## **Slots virtuais**

Nove nomes fixos, independentes da armadura real:

`HEAD · FACE · NECK · CHEST · BACK · WAIST · LEGS · FEET · HAND`

Cada um tem:

```json
"HEAD": { "defaultLimit": 1, "permission": "gc.slot.head" }
```

* **`defaultLimit`** — cosméticos que um jogador normal pode usar nesse slot.
* **`permission`** — o **node base** pro sistema de tiers.

### Aumentando um limite de slot

| Node | Efeito |
| :--- | :--- |
| `gc.slot.head.3` | Define o limite de HEAD como **3** (o mod pega o tier **mais alto** de 1 a 20 que o jogador tem). |
| `gc.slot.head.bypass` | Ilimitado (99) em HEAD. |
| `gc.extraslot.head.2` | **+2** em cima do limite normal (o maior `extraslot.head.N` único que o jogador tem). |
| `gc.extraslot.all.4` | **+4** em **todo** slot (somado em cima do extra específico do slot). |

`gc.slot.*` **substitui** o limite pelo valor do tier; `gc.extraslot.*` **soma** nele. Eles se acumulam: base `1` + `gc.slot.head.3` → `3`, depois + `gc.extraslot.all.2` → `5`.

---

## **Tipos de acessório**

Um **tipo** é uma categoria de texto livre que você atribui a um cosmético (o campo **Type** dele). Ele limita quantos cosméticos *daquela categoria* um jogador usa, independente do slot.

```json
"necklace": { "slot": "NECK", "limitPerPlayer": 1, "permission": "gc.type.necklace" }
```

* **`slot`** — informativo (a qual área do corpo esse tipo pertence).
* **`limitPerPlayer`** — máximo de cosméticos com esse tipo exato usados ao mesmo tempo.
* **`permission`** — node base pros tiers.

### Aumentando um limite de tipo

| Node | Efeito |
| :--- | :--- |
| `gc.type.necklace.2` | Aumenta o limite de necklace pra **2**. |
| `gc.type.necklace.bypass` | Ilimitado (99) pra necklaces. |

Um cosmético com o tipo `default` **não** tem limite de tipo — só o limite de slot dele se aplica.

---

## **Como uma checagem roda quando um jogador equipa**

1. O jogador é **dono** (ou tem o node `permission`, ou Dev Mode)? Se não → bloqueado.
2. **Contagem do slot** pro slot alvo vs. o limite de slot resolvido (`defaultLimit` → tier `gc.slot` → `+ extraslot`).
3. **Contagem do tipo** pro tipo do cosmético vs. o limite de tipo resolvido.

Se qualquer checagem falha, o jogador recebe uma mensagem e um som; nada é equipado.

Operadores e Dev Mode passam por cima de todos os limites de slot/tipo. O `/gc cosmetics equip` também força equipar ignorando limites.

---

## **Exemplo: um setup "3 chapéus pra VIP"**

`mainconfig.conf`:

```json
"HEAD": { "defaultLimit": 1, "permission": "gc.slot.head" }
```

LuckPerms:

```
lp group vip permission set gc.slot.head.3 true
```

Agora VIPs usam até 3 cosméticos de HEAD; todo mundo usa 1.
