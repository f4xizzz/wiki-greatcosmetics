# **Integrações**

---

O GreatCosmetics roda em **qualquer servidor Fabric** — ver [Dependências](Dependencies.pt.md) pra lista completa. Dois mods destravam recursos extras quando instalados junto:

* **[Integração com Cobblemon](Cobblemon Integration.pt.md)** — aba Party, Skins de Pokémon, bônus de Lure, Scanners, Heal Ability, Shiny & HA Radar, Shiny Effect.
* **[Integração com LuckPerms](LuckPerms Integration.pt.md)** — Chat Tags, página Chat Tags do Dev Studio, Granted Permissions por cosmético, Effect-Blocked Groups.

Os dois são opcionais e seguem a mesma regra:

!!! info "A regra de ouro"
    Nada no GreatCosmetics **exige** Cobblemon ou LuckPerms pra inicializar ou salvar dados. Campos que pertencem a uma dessas integrações (bônus de Lure, scanners, Granted Permissions, …) continuam gravados no arquivo de config do cosmético mesmo sem o mod correspondente instalado — só não fazem nada até ele estar presente. Adicione o mod depois, rode `/gc reload`, e tudo que já estava configurado liga na hora. Não precisa configurar de novo.

---

## **Outras integrações opcionais**

Pequenas demais pra precisar de página própria:

| Mod | Destrava | Sem ele |
| :--- | :--- | :--- |
| [**Player Animation Lib**](https://modrinth.com/mod/playeranimator) *(client-side, "playeranimator")* | Suprime totalmente a animação idle customizada de outro mod (ex: Emotecraft) enquanto o toggle **Breathing** do guarda-roupa está desligado. | O toggle Breathing ainda zera o balanço idle do próprio vanilla, mas a animação idle de um mod de animação de TERCEIROS (se o jogador tiver um instalado) continua tocando — não tem como mexer no sistema de animação de outro mod sem essa lib. |

Ver [Dependências](Dependencies.pt.md) pra MySQL e hospedagem de resource pack, que não são "integrações" nesse sentido — são backends alternativos com os quais o GreatCosmetics conversa direto.

---

!!! info "Precisa de outra integração?"
    Abra um ticket no nosso [Discord](https://discord.gg/GbbbNvQG3N) — a gente avalia e prioriza integrações pedidas.
