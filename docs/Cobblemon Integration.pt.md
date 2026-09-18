# **Integração com Cobblemon**

---

Precisa do **Cobblemon `1.8.0`** ou mais novo (ver [Dependências](Dependencies.pt.md)). Tudo abaixo fica escondido na UI ou silenciosamente inerte sem ele.

| Recurso | Onde | Detalhes |
| :--- | :--- | :--- |
| **Aba Party** | `/wardrobe` | Deixa o jogador navegar e aplicar [Skins de Pokémon](Pokemon Skins.pt.md) no time dele. |
| **Popup Cobblemon Effects** | Dev Studio → editor de cosmético → `>> Cobblemon Effects` | Guarda tudo abaixo. |
| **Bônus de Lure** | Popup Cobblemon Effects | Chance de shiny, IVs garantidos, ganho de EV, chance de captura, hidden ability, EXP, amizade, boost de tipo no spawn selvagem, bônus de pesca. Ver [Cobblemon Effects](Lure System.pt.md). |
| **Scanners** (IVs / Nature / Ability / Size / Dex) | Popup Cobblemon Effects | Mostram informação extra acima/ao lado de todo Pokémon próximo enquanto equipado. Ver [Cobblemon Effects § Scanners](Lure System.pt.md#scanners). |
| **Heal Ability** | Popup Cobblemon Effects | Cura a party inteira do jogador (HP/status/PP) num Shift-hold ou num clique nas Ações Rápidas. Ver [Special Effects](Attributes.pt.md#special-effects-habilidades-ativas). |
| **Shiny & HA Radar** | Popup Cobblemon Effects | Avisa o jogador quando um Pokémon selvagem shiny/Hidden-Ability está perto. Ver [Special Effects](Attributes.pt.md#special-effects-habilidades-ativas). |
| **Shiny Effect** | Popup Cobblemon Effects | Aplica a própria partícula + som de shiny do Cobblemon no *jogador*, usando o asset real do Cobblemon (não uma partícula genérica). |
| **Skins de Pokémon** | Aba Party / Dev Studio | Um sub-sistema inteiro de cosmético pra re-skinnar uma espécie de Pokémon (ver [Skins de Pokémon](Pokemon Skins.pt.md)) — o recurso inteiro precisa de Cobblemon por definição. |

---

## **Sem Cobblemon**

* A aba **Party** não aparece no guarda-roupa.
* O popup Cobblemon Effects (e tudo dentro dele) não aparece no Dev Studio.
* Qualquer valor de Lure/scanner/Heal Ability/Radar/Shiny Effect já salvo num cosmético continua no arquivo de config intocado — só não faz nada até o Cobblemon voltar.
* Todo o resto dos recursos de cosmético (models, sons, atributos, mochilas, cosméticos de armadura, efeitos de partícula, cosméticos de NPC, Tags, o guarda-roupa em si) funciona exatamente igual.
