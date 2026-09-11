# **Cobblemon Effects (Lure + Scanners)**

---

O editor **Cobblemon Effects** deixa um cosmético dar vantagens do **Cobblemon**: bônus de Lure (shiny, IVs garantidos, chance de captura, hidden abilities, EXP, ganho de EV, amizade, um boost de tipo no spawn selvagem e bônus de pesca) e quatro **Scanners** (IVs, Nature, Ability, Size).

Configure na seção **`>> Cobblemon Effects`** do editor de cosmético do [Dev Studio](Dev Studio.md). Cada campo tem tooltip por hover. A página inteira (e os campos abaixo) só aparece / faz alguma coisa num servidor com **Cobblemon** instalado.

---

## **Scanners**

Quatro toggles independentes. Enquanto o jogador veste um cosmético (ou um [cosmético de armadura](Armor Cosmetics.md)) com qualquer um deles ligado, informações de **todo Pokémon num raio de ~48 blocos** — selvagem incluso — aparecem flutuando perto do nome dele:

| Scanner | Mostra | Onde |
| :--- | :--- | :--- |
| **IVs Scanner** (`ivScanner`) | Seis linhas, uma stat por linha (`Health`, `Attack`, `Defense`, `Sp. Attack`, `Sp. Defense`, `Speed`), cada rótulo na sua própria cor em negrito. | Acima do nome. |
| **Nature Scanner** (`natureScanner`) | A nature do Pokémon. | Uma linha acima do nome (abaixo do bloco de IV, se os dois estiverem ligados). |
| **Ability Scanner** (`abilityScanner`) | A ability do Pokémon. | À **direita** do nome. |
| **Size Scanner** (`sizeScanner`) | A categoria de tamanho (XS/S/M/L/XL). | À **esquerda** do nome. |

Todos são **independentes do `enabled` do Lure** e uns dos outros — combine à vontade no mesmo cosmético. Dados de Pokémon selvagem (IVs, nature, ability, tamanho exato) simplesmente não existem no cliente, então o servidor calcula e empurra isso algumas vezes por segundo enquanto qualquer scanner está equipado.

---

## **Como os números funcionam**

* **`enabled`** precisa estar ligado pra qualquer bônus de *Lure* valer (não os Scanners).
* Os bônus de **todo** cosmético de Lure equipado são **somados** (diferente dos efeitos de velocidade/poção, que pegam o maior).
* Campos de "chance" são probabilidades `0.0`–`1.0` (`0.25` = 25%). Campos de "multiplier" multiplicam a quantidade base.
* Os rolls de shiny e IV acontecem **na captura**, não no spawn (uma decisão de design deliberada) — então o jogador tem que de fato capturar o Pokémon.
* **Affected Type** é a única exceção que mexe no **spawn** — ver abaixo.

---

## **HUD de cosméticos**

Enquanto o player veste qualquer cosmético que dá alguma coisa, uma HUD compacta aparece no **canto inferior direito** (fundo transparente, texto pequeno) listando o que os cosméticos equipados dão — em bullets: **Abilities** (voo, mochila, auto-feed, e qualquer Scanner ativo), **Effects** (efeitos de poção, rastro de partícula), **Lure**, **Fishing**. Os números de Lure/Fishing mostram o total **somado** que o servidor aplica. Scanners ativos ficam juntos numa linha, ex.: *"IVs, Nature, Size Scanner"*. Se a lista fica grande, ela encolhe sozinha pra nunca cobrir mais de ~metade da tela. Liga/desliga pro servidor todo com `lureHud` no [Main Config](Main Config.md) (ligado por padrão), ou esconde só pra você na aba **Preview** do guarda-roupa.

---

## **Campos**

| Campo | Tipo | Efeito | Quando |
| :--- | :--- | :--- | :--- |
| **Affected Type** (`lureTYPE`) | texto | **Aumenta** o peso de spawn de espécies desse tipo no **seu** pool de spawn selvagem (espécies desse tipo ganham um multiplicador de peso grande, o resto um multiplicador pequeno) — não filtra mais os outros tipos, então os spawns continuam acontecendo na taxa normal, sem "buracos" enquanto está ativo. Os spawns de outros jogadores não mudam, e o seu time / NPCs nunca são afetados. Aceita nome ou id do tipo (ex.: `fire`). | No spawn |
| **Shiny Multiplier** (`lureShinyMultiplier`) | chance | Chance de re-rolar uma captura não-shiny pra shiny | Na captura |
| **Lure IV** (`lureIV`) | contagem | Número de IVs forçados a 31 na captura | Na captura |
| **Per-IV Perfect Chance** (`lureChanceIV`) | chance | Chance, **por IV**, de cada um dos 6 IVs vir 31 (rolagem independente pra cada stat, além dos garantidos pelo Lure IV) | Na captura |
| **Hidden Ability Multiplier** (`lureHiddenAbilityMultiplier`) | chance | Chance de dar ao Pokémon capturado a hidden ability | Na captura |
| **Ultra Rare Multiplier** (`lureUltraRAREMultiplier`) | chance | Chance de subir um spawn pro bucket "ultra raro" | No spawn |
| **Capture Chance** (`lureChanceDeCaptura`) | chance | Chance de transformar uma captura **falha** em sucesso | No arremesso da ball |
| **EXP Multiplier** (`lureEXP`) | multiplier | Experiência extra pro Pokémon que lutou (`0.5` = +50%) | No ganho de EXP |
| **Exp Share to Party** (`lureExpAllMultiplier`) | on/off | Ligado, cada outro Pokémon **vivo** da party também recebe o XP cheio que o Pokémon ativo ganhou (com o EXP Multiplier incluso). **Não** vale pra XP de doce (Rare/Exp Candy). No editor aparece como um botão liga/desliga. | No ganho de EXP |
| **EV Multiplier** (`lureEV`) | multiplier | EVs extras ganhos em batalha (`0.5` = +50%) | No ganho de EV |
| **Friendship Multiplier** (`lureAmizadeMultiplier`) | multiplier | Amizade extra ganha | Na atualização de amizade |
| **Fishing Shiny** (`lurePescaShiny`) | chance | Chance de shiny extra, só na pesca (soma com o Shiny Multiplier) | Ao pescar um Pokémon |
| **Fishing IV** (`lurePescaIv`) + **Fishing Per-IV Perfect Chance** (`lurePescaIvChance`) | contagem + chance | Igual ao Lure IV / Per-IV Perfect Chance, só que só na pesca | Ao pescar um Pokémon |
| **Fishing Speed** (`lurePescaVelocidade`) | valor | Adiciona níveis do encantamento "Lure" do Cobblemon à vara pra fisgadas mais rápidas | Ao lançar a vara |
| **IVs / Nature / Ability / Size Scanner** | on/off | Ver [Scanners](#scanners) acima. Independente do `enabled`. | Enquanto equipado |

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
