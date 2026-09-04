# **Skins de Pokémon**

---

Uma **Skin de Pokémon** aplica um **aspect** do Cobblemon (tipo `summer`, `clone`, `mega`) a um dos Pokémon do time do jogador, mudando o visual dele. Os jogadores gerenciam na aba **Party** do guarda-roupa.

Arquivo de catálogo: **`config/GreatCosmetics/pokeskins.json`**. Exige o **Cobblemon**.

---

## **Campos da skin**

```json
[
  {
    "id": "pikachu_summer",
    "displayName": "Pikachu Praiano",
    "species": "pikachu",
    "aspect": "summer",
    "cooldownMinutes": 60,
    "altForms": [],
    "group": ""
  }
]
```

| Campo | Significado |
| :--- | :--- |
| **id** | Identificador único. Usado por `/gc giveskin`. |
| **displayName** | Nome MiniMessage mostrado na lista da Party. |
| **species** | Nome da espécie do Cobblemon a que a skin se aplica — o jogador só pode usar nessa espécie. |
| **aspect** | A string de aspect do Cobblemon aplicada ao Pokémon. Pode ser um aspect simples (`summer`), uma forma (`f=alola`), ou uma feature composta (`battle_bond=ash`). |
| **cooldownMinutes** | Minutos antes de o jogador poder reaplicar essa skin. `0` = sem cooldown. |
| **altForms** | Lista opcional de aspects extras que o **preview** pode ciclar (mega, gmax, regional…). Só afeta o botão de preview; a skin aplicada continua sendo `aspect`. |
| **group** | Nome de tema opcional (`"League of Legends"`, `"Arcane"`…) usado pra agrupar visualmente skins relacionadas na lista. As cores vêm do `skin_groups.json`. |

---

## **Usando uma skin (jogador)**

1. `/wardrobe` → aba **Party**.
2. Escolha um slot do time com as setas **`<` / `>`**.
3. Navegue na lista de skins; as incompatíveis (espécie errada / não possuída) mostram um status vermelho.
4. **Preview** (👁) mostra a skin num Pokémon dummy — cicle pose, forma alternativa e shiny antes de confirmar.
5. Clique numa skin compatível, possuída e fora de cooldown pra aplicar.

O toggle **DEV** (precisa de `gc.dev` / OP) mostra toda skin como possuída pra teste.

---

## **Grupos & cores de skin**

`config/GreatCosmetics/skin_groups.json` mapeia um nome de grupo pra uma cor usada no cabeçalho dele na lista:

```json
{ "League of Legends": "#c8aa6e", "Arcane": "#3b0e6d" }
```

---

## **Concedendo skins**

| Comando | Efeito |
| :--- | :--- |
| `/gc giveskin <skin_id> [jogador]` | Desbloqueia a skin pro alvo. |
| `/gc removeskin <skin_id> [jogador]` | Remove ela. |

A posse e os cooldowns por skin ficam guardados no banco de dados.

---

## **Limpando skins**

No Dev Mode, a aba Party tem botões **Clear Current** (este Pokémon) e **Clear Party** (todos os seis) que tiram todo aspect de skin do GreatCosmetics. Os jogadores também podem só aplicar uma skin diferente.
