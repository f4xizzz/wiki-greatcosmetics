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

### Bônus por jogador: `/gc extraslot`

O `gc.extraslot.*` acima é concedido via **LuckPerms**, então vale pro grupo inteiro de uma vez. O GreatCosmetics também tem uma segunda forma, independente, de somar bônus de slot — mirada em **um jogador específico** e guardada no banco de dados em vez de um node de permissão:

**`/gc extraslot <jogador> <slot|ALL> add|set|remove <quantidade>`**

* **`add <quantidade>`** — soma ao bônus que o jogador já tem nesse slot.
* **`set <quantidade>`** — sobrescreve pra exatamente esse valor.
* **`remove <quantidade>`** — subtrai dele.
* `<slot>` é um dos nove nomes de slot (case-insensitive) ou `ALL` pra afetar todo slot de uma vez.
* Permissão: `gc.command.extraslot`.

!!! tip "Dois bônus, e eles se acumulam"
    Um node `gc.extraslot.head.2` no LuckPerms e o comando `/gc extraslot Steve head add 2` somam +2 em HEAD cada um — e eles se somam entre si. Use o node de permissão pra bonificar um rank inteiro; use `/gc extraslot` pra presentear slots bônus a um jogador específico sem precisar criar um rank pra isso.

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
| `gc.extratypeslot.necklace.2` | **+2** em cima do limite normal (o maior `extratypeslot.necklace.N` único que o jogador tem). |
| `gc.extratypeslot.all.4` | **+4** a **todo** tipo (somado em cima do extra específico do tipo). |

`gc.type.*` **substitui** o limite pelo valor do tier; `gc.extratypeslot.*` **soma** nele. Eles se acumulam do mesmo jeito que os nodes de slot: base `1` + `gc.type.necklace.2` → `2`, depois + `gc.extratypeslot.all.1` → `3`.

Um cosmético com o tipo `default` **não** tem limite de tipo — só o limite de slot dele se aplica.

### Bônus de tipo por jogador: `/gc extratypeslot`

Espelho exato do `/gc extraslot`, mas pra **tipos de acessório** em vez de slots virtuais:

**`/gc extratypeslot <jogador> <tipo|ALL> add|set|remove <quantidade>`**

* Mesma semântica de `add` / `set` / `remove` do `/gc extraslot`, guardada **por jogador no banco de dados**.
* `<tipo>` é qualquer id de tipo definido na sua config (case-insensitive) ou `ALL` pra todo tipo de uma vez.
* Permissão: `gc.command.extratypeslot`.

!!! tip "Dois bônus, e eles se acumulam"
    Um node `gc.extratypeslot.necklace.2` no LuckPerms e o comando `/gc extratypeslot Steve necklace add 2` somam +2 no limite de necklace cada um — e eles se somam entre si, igualzinho ao `gc.extraslot.*` vs. `/gc extraslot` pros slots.

---

## **Como uma checagem roda quando um jogador equipa**

1. O jogador é **dono** (ou tem o node `permission`, ou Dev Mode)? Se não → bloqueado.
2. **Contagem do slot** pro slot alvo vs. o limite de slot resolvido (`defaultLimit` → tier `gc.slot` → `+ bônus de extraslot`, vindos de nodes de permissão e/ou de `/gc extraslot`).
3. **Contagem do tipo** pro tipo do cosmético vs. o limite de tipo resolvido (`limitPerPlayer` → tier `gc.type` → `+ bônus de extratypeslot`, vindos de nodes de permissão e/ou de `/gc extratypeslot`).

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
