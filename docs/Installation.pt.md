# **Instalação**

---

!!! info "Fabric **e** NeoForge"
    O GreatCosmetics tem versão pros dois loaders. Escolha o jar que combina com o seu servidor — `greatcosmetics-fabric-<versão>.jar` ou `greatcosmetics-neoforge-<versão>.jar`. O suporte a NeoForge é recente; se algo se comportar diferente do Fabric, avise no [Discord](https://discord.gg/aDCgBbvRe5).

## **Requisitos do Servidor**

| Requisito | Fabric | NeoForge |
| :--- | :--- | :--- |
| Minecraft | 1.21.1 | 1.21.1 |
| Java | 21 ou superior | 21 ou superior |
| Loader | Fabric Loader 0.16 ou superior | NeoForge 21.1.133 ou superior |
| Cobblemon | 1.7.3 | 1.7.3 |
| Runtime Kotlin | Fabric Language Kotlin `1.13.13+kotlin.2.4.10` ou superior | Kotlin for Forge `5.7.0` ou superior |
| API | Fabric API `0.116.9+1.21.1` ou superior | — |
| Architectury API | `13.0.0` ou superior | `13.0.0` ou superior |

Links de download em [Dependências](Dependencies.md).

---

## **Passo 1 — Coloque o jar**

1. Coloque o `.jar` do GreatCosmetics do seu loader na pasta `mods/` do servidor, junto com Cobblemon, Architectury API e o runtime do Kotlin (Fabric Language Kotlin no Fabric, Kotlin for Forge no NeoForge — mais a Fabric API no Fabric).
2. Inicie (ou reinicie) o servidor.
3. No primeiro boot o mod cria a pasta **`config/GreatCosmetics/`** com todos os arquivos de config padrão, e gera um cosmético inicial pra você confirmar que carregou.

!!! note "Mesmo jar pros jogadores"
    Só existe um jar — dê pros jogadores exatamente o mesmo arquivo que você colocou no servidor (mesma versão). A Dev Studio e as outras ferramentas de admin já são restritas a operadores e jogadores com a permissão específica, então não tem build separada e enxuta pra distribuir.

---

## **Passo 2 — Configure o básico**

Abra `config/GreatCosmetics/` e ajuste:

| Arquivo | O que definir | Página |
| :--- | :--- | :--- |
| `mainconfig.conf` | Modo do banco de dados, limites de slot/tipo, resource pack forçado, comandos de boot | [Config Principal](Main Config.md) |
| `lang/*.json` | Idioma, cores e toda mensagem que o mod mostra | [Idioma & MiniMessage](Language.md) |

Todo o resto (cosméticos, tags, efeitos, skins) é melhor editar **dentro do jogo** — ver [Dev Studio](Dev Studio.md).

---

## **Passo 3 — Ative a licença**

Num **servidor dedicado**, o GreatCosmetics fica travado até você ativar uma chave de licença:

1. Entre no seu servidor como operador.
2. Rode: `/gc activation GREATCOSMETICS-XXXX-XXXX`

Isso vincula a chave à instância do seu servidor e cria `config/GreatCosmetics/license.json`.

!!! warning "Um servidor por chave"
    Na primeira ativação a chave é vinculada àquela instância de servidor. O seu IP público pode mudar sem quebrar a ativação, mas a chave não pode ser compartilhada nem rodar num segundo servidor diferente. Fale com o suporte pra migrar uma chave pra outra máquina.

!!! info "Singleplayer / LAN"
    No singleplayer ou num mundo LAN integrado o mod fica **sempre ativo** — sem chave. A ativação é um conceito de servidor dedicado.

Detalhes completos em [Licença & Ativação](License.md).

---

## **Passo 4 — Reload**

Depois de editar arquivos de config, aplique tudo sem reiniciar:

`/gc reload`

Isso recarrega todas as configs, recalcula os dados de modelo, reenvia o resource pack pros jogadores online e re-sincroniza o catálogo inteiro.

---

### Pronto — o guarda-roupa está no ar. Os jogadores abrem com `/wardrobe`.
