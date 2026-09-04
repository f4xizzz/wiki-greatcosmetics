# **Cosméticos em NPC**

---

Você pode equipar cosméticos do GreatCosmetics em **qualquer entidade viva** — NPCs do EasyNPC, Armor Stands, mobs — não só em jogadores. O mod renderiza o cosmético na entidade do mesmo jeito que renderiza num jogador, então partes 3D / GeckoLib personalizadas aparecem corretamente.

O estado em runtime fica em **`config/greatcosmetics/npc_cosmetics.json`** (chaveado por UUID da entidade) e é re-sincronizado pros jogadores no join e no `/gc reload`.

---

## **Equipando**

1. Fique a até **5 blocos** e olhe diretamente pra entidade.
2. Rode:

    `/gc npc equip <cosmetic_id>`

O cosmético é registrado no UUID daquela entidade e aparece pra todo mundo.

!!! note "Por que não `/data` ou o slot de armadura?"
    O sistema de cosméticos nunca lê o slot de equipamento real da entidade — ele renderiza puramente do seu próprio registro. Colocar o item no slot de armadura mostraria um item chapado/quebrado (ou nada num NPC cujo renderer ignora esse slot). Sempre use `/gc npc equip`.

---

## **Removendo**

Olhe pra entidade e rode:

`/gc npc remove <slot>`

`<slot>` é um de `head, face, neck, chest, back, waist, legs, feet, hand`. Isso limpa todo cosmético daquele slot virtual no alvo.

---

## **Pegando o UUID de uma entidade**

`/gc uuid` — olhe pra uma entidade a até 5 blocos e rode. O UUID é impresso com um link de **clique-pra-copiar**, pra usar em outras configs ou datapacks.

---

## **Permissões**

| Node | Comando |
| :--- | :--- |
| `gc.command.npc.equip` | `/gc npc equip` |
| `gc.command.npc.remove` | `/gc npc remove` |
| `gc.command.uuid` | `/gc uuid` |
