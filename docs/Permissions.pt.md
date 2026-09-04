# **Permissões**

---

O GreatCosmetics usa a **API de permissões do Fabric** (fornecida pelo **LuckPerms**). Um jogador passa numa checagem se for operador de verdade (`ops.json`) **ou** tiver o node. Sem um mod de permissões, só operadores passam e todas as Tags de grupo viram só prévia.

---

## **Nodes de Comando**

| Node | Comando |
| :--- | :--- |
| `gc.command.wardrobe.self` | `/wardrobe` |
| `gc.command.wardrobe.other` | `/wardrobe <jogador>` |
| `gc.command.wardrobe.setbackground` | `/gc wardrobe setbackground` |
| `gc.command.give` | `/gc give` |
| `gc.command.giveitem` | `/gc giveitem` |
| `gc.command.remove` | `/gc remove` |
| `gc.command.cosmetics.equip` / `.unequip` | `/gc cosmetics equip` / `unequip` |
| `gc.command.giveskin` / `gc.command.removeskin` | `/gc giveskin` / `removeskin` |
| `gc.command.tags.give` / `gc.command.tags.remove` | `/gc tags give` / `remove` |
| `gc.command.npc.equip` / `gc.command.npc.remove` | `/gc npc equip` / `remove` |
| `gc.command.uuid` | `/gc uuid` |
| `gc.command.reload` / `gc.command.debug` / `gc.command.inspect` | `/gc reload` / `debug` / `inspect` |
| `gc.command.activation` | `/gc activation` |

---

## **Acesso ao Dev Studio**

| Node | Concede |
| :--- | :--- |
| `gc.dev` | Dev Studio completo: criar/editar/apagar cosméticos, efeitos, tipos, slots e config do servidor. Também deixa o jogador ligar o **Dev Mode** no guarda-roupa (previsualizar todo cosmético/tag sem possuir). |
| `gc.perm.devmode` | Só o bypass de **Dev Mode** — equipar qualquer cosmético pra teste sem possuir. O nome do node é configurável via `devModePermission` no `mainconfig.conf`. |

!!! warning
    A **aba Dev Studio** exige, além disso, que o jogador seja **operador de verdade**. Só o `gc.dev` revela os controles de admin dentro das abas Tags / Party, mas não o painel completo do Dev Studio.

---

## **Possuindo Cosméticos**

* Um cosmético com o campo **`permission`** preenchido só aparece/equipa pra quem tem esse node exato (ou quem desbloqueou via `/gc give`, ou quem tem Dev Mode).
* Fora isso, os jogadores desbloqueiam cosméticos por `/gc give`, pelo item físico (`/gc giveitem`), ou pela conversão automática de armadura.

---

## **Limites de Slot**

Cada slot virtual tem um limite base (`defaultLimit` no `mainconfig.conf`). Os jogadores aumentam com nodes em tiers a partir da base `permission` do slot (padrão `gc.slot.<slot>`):

| Padrão de node | Efeito |
| :--- | :--- |
| `gc.slot.<slot>.<N>` | Define o limite **absoluto** do slot como **N** (vale o tier mais alto de 1 a 20 que o jogador tiver). |
| `gc.slot.<slot>.bypass` | Ilimitado (99) nesse slot. |
| `gc.extraslot.<slot>.<N>` | **Soma** N itens extras em cima do limite normal. |
| `gc.extraslot.all.<N>` | Soma N itens extras a **todo** slot. |

`<slot>` é minúsculo: `head, face, neck, chest, back, waist, legs, feet, hand`.

---

## **Limites de Tipo**

Os *tipos* de acessório (ex: `necklace`, `scarf`) também têm `limitPerPlayer` e uma base `permission` (padrão `gc.type.<type>`):

| Padrão de node | Efeito |
| :--- | :--- |
| `gc.type.<type>.<N>` | Aumenta o limite por jogador desse tipo pra **N**. |
| `gc.type.<type>.bypass` | Ilimitado (99) pra esse tipo. |

---

## **Nodes de Tag**

* Cada Tag lista o seu próprio array `permissions` — um jogador "possui" uma Tag personalizada se tiver **qualquer** node dessa lista (ou recebeu via `/gc tags give`).
* **Tags de Grupo** são possuídas automaticamente por estar no **grupo do LuckPerms** correspondente.

Ver [Tags](Tags.md).
