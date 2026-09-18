# **Integração com LuckPerms**

---

O GreatCosmetics usa a **Fabric permissions API**, que o LuckPerms implementa — ver [Permissões](Permissions.pt.md) pra referência completa de nodes. Esta página é o resumo de "o que precisa do LuckPerms especificamente".

| Recurso | Onde | Detalhes |
| :--- | :--- | :--- |
| **Chat Tags** | `/wardrobe` → aba Tags | Seletor de prefixo; possuir uma Tag **custom** precisa de um node de permissão, possuir uma Tag de **grupo** precisa de participação num grupo do LuckPerms. Ver [Tags](Tags.pt.md). |
| **Dev Studio → Chat Tags** | Dev Studio | O editor de Tags in-game — os mesmos dados da aba Tags. |
| **Granted Permissions** *(por cosmético)* | Dev Studio → editor de cosmético | Uma lista separada por vírgula de nodes de permissão aplicados como permissões **transient** (só na sessão) do LuckPerms enquanto o cosmético está equipado e o próprio gate `permission` dele passa. Removidos ao desequipar. Ver [Permissões § Permissões e Tags concedidas POR um cosmético](Permissions.pt.md#permissoes-e-tags-concedidas-por-um-cosmetico). |
| **Effect-Blocked Groups** | Dev Studio → Server Config | Uma lista separada por vírgula, pro servidor inteiro, de grupos do LuckPerms cujos jogadores **não recebem efeito de cosmético nenhum** — partículas, efeitos de poção, voo, velocidade, Lure, scanners, permissões/tags concedidas. O modelo do cosmético continua renderizando; só os *efeitos de gameplay* são suprimidos. Útil pra um rank "só cosmético, sem vantagem de jogo". Vazio por padrão (ninguém bloqueado). |
| **Limites de slot/tipo, nodes de comando** | Em todo lugar | Nodes em camadas tipo `gc.slot.<slot>.<N>` ou `gc.command.wardrobe.self`. Ver [Permissões](Permissions.pt.md). |

!!! note "Minecraft Tags não precisa de LuckPerms"
    O campo **Minecraft Tags** de um cosmético (scoreboard `/tag` vanilla) é completamente independente do LuckPerms — funciona em qualquer servidor Fabric. Só o **Granted Permissions** (nodes de permissão de verdade) precisa de um plugin de permissão por trás.

---

## **Sem LuckPerms**

* Só operadores reais do servidor (`ops.json`) passam em qualquer checagem de permissão — a Fabric permissions API cai pro fallback "só OP".
* A aba **Tags** e a página **Chat Tags** do Dev Studio ficam totalmente escondidas.
* O campo **Granted Permissions** de um cosmético continua salvando mas nunca aplica nada (sem plugin de permissão pra receber os nodes). O campo **Minecraft Tags** continua funcionando normalmente (ver nota acima).
* **Effect-Blocked Groups** não tem contra o que checar participação de grupo, então vira um no-op.
* Checagens de permissão de slot/tipo/comando continuam funcionando (qualquer backend da Fabric permissions API além do LuckPerms também funcionaria aqui) — o LuckPerms é só o mais comum que a maioria dos servidores já roda.
