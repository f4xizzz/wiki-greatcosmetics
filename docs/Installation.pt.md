# **Instalação**

---

## **Requisitos do Servidor**

| Requisito | Versão |
| :--- | :--- |
| Minecraft | 1.21.1 |
| Fabric Loader | 0.18.3 ou superior |
| Fabric API | 0.116.9+1.21.1 ou superior |
| Java | 21 ou superior |
| Cobblemon | 1.7.3 |
| Fabric Language Kotlin | 1.13.13+kotlin.2.4.10 ou superior |

Links de download em [Dependências](Dependencies.md).

---

## **Passo 1 — Coloque o jar**

1. Coloque o `.jar` do GreatCosmetics na pasta `mods/` do seu servidor (junto com Cobblemon, Fabric API e Fabric Language Kotlin).
2. Inicie (ou reinicie) o servidor.
3. No primeiro boot o mod cria a pasta **`config/greatcosmetics/`** com todos os arquivos de config padrão, e gera um cosmético inicial pra você confirmar que carregou.

!!! note "Jar client-only"
    A build também gera um `*-client.jar` com o **Dev Studio removido** e sem os drivers de banco. Dê esse pros seus jogadores no modpack; mantenha o jar completo no servidor. Os dois têm que ser da mesma versão.

---

## **Passo 2 — Configure o básico**

Abra `config/greatcosmetics/` e ajuste:

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

Isso vincula a chave ao IP do seu servidor e cria `config/greatcosmetics/license.json`.

!!! warning "Um servidor por chave"
    O sistema de segurança vincula a chave permanentemente ao **primeiro IP** que a validar. Compartilhamento e múltiplas ativações não são possíveis. Chaves `-DEV-` são a exceção (sem trava de IP, sem checagem de hash do jar).

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
