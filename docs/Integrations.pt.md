# **Integrações**

---

O GreatCosmetics roda em **qualquer servidor Fabric** — ver [Dependências](Dependencies.pt.md) pra lista completa. Esta página é o mapa do que muda quando dois mods específicos também estão instalados: **Cobblemon** e **LuckPerms**. Os dois são opcionais e seguem a mesma regra:

!!! info "A regra de ouro"
    Nada no GreatCosmetics **exige** Cobblemon ou LuckPerms pra inicializar ou salvar dados. Campos que pertencem a uma dessas integrações (bônus de Lure, scanners, Granted Permissions, …) continuam gravados no arquivo de config do cosmético mesmo sem o mod correspondente instalado — só não fazem nada até ele estar presente. Adicione o mod depois, rode `/gc reload`, e tudo que já estava configurado liga na hora. Não precisa configurar de novo.

---

## **Cobblemon**

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

### **Sem Cobblemon**

* A aba **Party** não aparece no guarda-roupa.
* O popup Cobblemon Effects (e tudo dentro dele) não aparece no Dev Studio.
* Qualquer valor de Lure/scanner/Heal Ability/Radar/Shiny Effect já salvo num cosmético continua no arquivo de config intocado — só não faz nada até o Cobblemon voltar.
* Todo o resto dos recursos de cosmético (models, sons, atributos, mochilas, cosméticos de armadura, efeitos de partícula, cosméticos de NPC, Tags, o guarda-roupa em si) funciona exatamente igual.

---

## **LuckPerms**

O GreatCosmetics usa a **Fabric permissions API**, que o LuckPerms implementa — ver [Permissões](Permissions.pt.md) pra referência completa de nodes. Esta seção é o resumo de "o que precisa do LuckPerms especificamente".

| Recurso | Onde | Detalhes |
| :--- | :--- | :--- |
| **Chat Tags** | `/wardrobe` → aba Tags | Seletor de prefixo; possuir uma Tag **custom** precisa de um node de permissão, possuir uma Tag de **grupo** precisa de participação num grupo do LuckPerms. Ver [Tags](Tags.pt.md). |
| **Dev Studio → Chat Tags** | Dev Studio | O editor de Tags in-game — os mesmos dados da aba Tags. |
| **Granted Permissions** *(por cosmético)* | Dev Studio → editor de cosmético | Uma lista separada por vírgula de nodes de permissão aplicados como permissões **transient** (só na sessão) do LuckPerms enquanto o cosmético está equipado e o próprio gate `permission` dele passa. Removidos ao desequipar. Ver [Permissões § Permissões e Tags concedidas POR um cosmético](Permissions.pt.md#permissoes-e-tags-concedidas-por-um-cosmetico). |
| **Effect-Blocked Groups** | Dev Studio → Server Config | Uma lista separada por vírgula, pro servidor inteiro, de grupos do LuckPerms cujos jogadores **não recebem efeito de cosmético nenhum** — partículas, efeitos de poção, voo, velocidade, Lure, scanners, permissões/tags concedidas. O modelo do cosmético continua renderizando; só os *efeitos de gameplay* são suprimidos. Útil pra um rank "só cosmético, sem vantagem de jogo". Vazio por padrão (ninguém bloqueado). |
| **Limites de slot/tipo, nodes de comando** | Em todo lugar | Nodes em camadas tipo `gc.slot.<slot>.<N>` ou `gc.command.wardrobe.self`. Ver [Permissões](Permissions.pt.md). |

!!! note "Minecraft Tags não precisa de LuckPerms"
    O campo **Minecraft Tags** de um cosmético (scoreboard `/tag` vanilla) é completamente independente do LuckPerms — funciona em qualquer servidor Fabric. Só o **Granted Permissions** (nodes de permissão de verdade) precisa de um plugin de permissão por trás.

### **Sem LuckPerms**

* Só operadores reais do servidor (`ops.json`) passam em qualquer checagem de permissão — a Fabric permissions API cai pro fallback "só OP".
* A aba **Tags** e a página **Chat Tags** do Dev Studio ficam totalmente escondidas.
* O campo **Granted Permissions** de um cosmético continua salvando mas nunca aplica nada (sem plugin de permissão pra receber os nodes). O campo **Minecraft Tags** continua funcionando normalmente (ver nota acima).
* **Effect-Blocked Groups** não tem contra o que checar participação de grupo, então vira um no-op.
* Checagens de permissão de slot/tipo/comando continuam funcionando (qualquer backend da Fabric permissions API além do LuckPerms também funcionaria aqui) — o LuckPerms é só o mais comum que a maioria dos servidores já roda.

---

## **Outras integrações opcionais**

| Mod | Destrava | Sem ele |
| :--- | :--- | :--- |
| [**Player Animation Lib**](https://modrinth.com/mod/playeranimator) *(client-side, "playeranimator")* | Suprime totalmente a animação idle customizada de outro mod (ex: Emotecraft) enquanto o toggle **Breathing** do guarda-roupa está desligado. | O toggle Breathing ainda zera o balanço idle do próprio vanilla, mas a animação idle de um mod de animação de TERCEIROS (se o jogador tiver um instalado) continua tocando — não tem como mexer no sistema de animação de outro mod sem essa lib. |

Ver [Dependências](Dependencies.pt.md) pra MySQL e hospedagem de resource pack, que não são "integrações" nesse sentido — são backends alternativos com os quais o GreatCosmetics conversa direto.

---

!!! info "Precisa de outra integração?"
    Abra um ticket no nosso [Discord](https://discord.gg/GbbbNvQG3N) — a gente avalia e prioriza integrações pedidas.
