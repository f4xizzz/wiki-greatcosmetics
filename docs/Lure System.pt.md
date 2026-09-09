# **Sistema de Lure**

---

O sistema **Lure** deixa um cosmético dar bônus de gameplay do **Cobblemon**: melhores chances de shiny, IVs garantidos, chance de captura, hidden abilities, EXP, amizade e bônus de pesca.

Configure na seção **`>> Configure LURE`** do editor de cosmético do [Dev Studio](Dev Studio.md). Só faz algo com o **Cobblemon** instalado.

---

## **Como os números funcionam**

* **`enabled`** precisa estar ligado pra qualquer bônus valer.
* Os bônus de **todo** cosmético de Lure equipado são **somados** (diferente dos efeitos de velocidade/poção, que pegam o maior).
* Campos de "chance" são probabilidades `0.0`–`1.0` (`0.25` = 25%). Campos de "multiplier" multiplicam a quantidade base.
* Os rolls de shiny e IV acontecem **na captura**, não no spawn (uma decisão de design deliberada) — então o jogador tem que de fato capturar o Pokémon.
* **Affected Type** é a única exceção que mexe no **spawn**: ele filtra as espécies selvagens que aparecem em volta de você.

---

## **HUD de Lure**

Enquanto o player estiver usando um ou mais cosméticos de Lure (ou armaduras-cosmético) com `enabled: true`, aparece uma coluna à **direita da hotbar** com os bônus **somados** — os mesmos totais que o servidor aplica de verdade. Some quando não tem Lure ativo. Liga/desliga pro servidor todo com `lureHud` no [Main Config](Main Config.md) (ligado por padrão).

---

## **Campos**

| Campo | Tipo | Efeito | Quando |
| :--- | :--- | :--- | :--- |
| **Affected Type** (`lureTYPE`) | texto | Enquanto ativo, só espécies desse tipo ficam elegíveis no **seu** pool de spawn selvagem — o Cobblemon então spawna normalmente entre o que sobrou, na taxa normal. Os spawns de outros jogadores não mudam, e o seu time / NPCs nunca são afetados. Se **nenhuma** espécie daquele tipo puder spawnar no seu bioma, nada spawna. Aceita nome ou id do tipo (ex.: `fire`). | No spawn |
| **Shiny Multiplier** (`lureShinyMultiplier`) | chance | Chance de re-rolar uma captura não-shiny pra shiny | Na captura |
| **Lure IV** (`lureIV`) | contagem | Número de IVs forçados a 31 na captura | Na captura |
| **Per-IV Perfect Chance** (`lureChanceIV`) | chance | Chance, **por IV**, de cada um dos 6 IVs vir 31 (rolagem independente pra cada stat, além dos garantidos pelo Lure IV) | Na captura |
| **Hidden Ability Multiplier** (`lureHiddenAbilityMultiplier`) | chance | Chance de dar ao Pokémon capturado a hidden ability | Na captura |
| **Ultra Rare Multiplier** (`lureUltraRAREMultiplier`) | chance | Chance de subir um spawn pro bucket "ultra raro" | No spawn |
| **Capture Chance** (`lureChanceDeCaptura`) | chance | Chance de transformar uma captura **falha** em sucesso | No arremesso da ball |
| **EXP Multiplier** (`lureEXP`) | multiplier | Experiência extra pro Pokémon que lutou (`0.5` = +50%) | No ganho de EXP |
| **Exp Share to Party** (`lureExpAllMultiplier`) | on/off | Ligado, cada outro Pokémon **vivo** da party também recebe o XP cheio que o Pokémon ativo ganhou (com o EXP Multiplier incluso). **Não** vale pra XP de doce (Rare/Exp Candy). No editor aparece como um botão liga/desliga. | No ganho de EXP |
| **Friendship Multiplier** (`lureAmizadeMultiplier`) | multiplier | Amizade extra ganha | Na atualização de amizade |
| **Fishing Shiny** (`lurePescaShiny`) | chance | Chance de shiny extra, só na pesca (soma com o Shiny Multiplier) | Ao pescar um Pokémon |
| **Fishing IV** (`lurePescaIv`) + **Fishing Per-IV Perfect Chance** (`lurePescaIvChance`) | contagem + chance | Igual ao Lure IV / Per-IV Perfect Chance, só que só na pesca | Ao pescar um Pokémon |
| **Fishing Speed** (`lurePescaVelocidade`) | valor | Adiciona níveis do encantamento "Lure" do Cobblemon à vara pra fisgadas mais rápidas | Ao lançar a vara |

---

## **Ainda não implementado**

* **EV Multiplier** (`lureEV`) — o ganho de EV é decidido dentro da lógica de batalha do Cobblemon, que não expõe um hook.

---

## **Exemplo: um chapéu "Shiny Charm"**

```json
"lure": {
  "enabled": true,
  "lureShinyMultiplier": 0.05,
  "lureChanceIV": 0.25,
  "lureIV": 2
}
```

Usar isso dá +5% de chance de shiny numa captura, 2 IVs perfeitos garantidos e +25% de chance **em cada um** dos outros 4 IVs virem 31. O tooltip do guarda-roupa lista todos os bônus ativos automaticamente.
