# **Idioma & MiniMessage**

---

Todo texto que o mod mostra a um jogador — rótulos de GUI, feedback de chat, nomes e lore de item, mensagens de action bar — fica em JSON editável em **`config/GreatCosmetics/lang/`**. Não existe um toggle de "idioma" embutido: você edita os valores pro idioma, texto e cores que quiser.

Linhas de log de console **não** ficam aqui — elas continuam em inglês dentro do código.

---

## **Os arquivos**

Um arquivo por área. As chaves são namespaced por arquivo (`commands.reload.start`, `accessories.category.head`, …).

| Arquivo | Cobre |
| :--- | :--- |
| `general.json` | Erros compartilhados, o fluxo do `/gc reload`, mensagens de licença |
| `commands.json` | Feedback de `/gc *` e `/wardrobe *` |
| `messages.json` | Chat / action-bar servidor → jogador (equipar, voo, tags, efeitos, skins, conversão de armadura, kick de join) |
| `items.json` | Nome-fallback do item cosmético, lore, linhas de atributo de Lure, tooltip do Scanner |
| `wardrobe.json` | Título da tela, nomes das abas, título do painel, os toggles da aba Preview |
| `accessories.json` | Nomes de categoria, "Clear All", placeholder de busca, toda linha de tooltip |
| `party.json` | Lista de Skins de Pokémon, modo preview, rótulos de pose / forma / shiny |
| `tags.json` | Cabeçalhos do menu de Tags, tooltips, rótulos de campo do editor |
| `backpack.json` | Título do seletor de mochila, o overlay "Page X/Y" |
| `devstudio.json` | Todo rótulo, divisor, botão e popup do Dev Studio |

Ao carregar, o mod preenche as chaves que **faltam** com os padrões em inglês e regrava o arquivo — os seus valores customizados nunca são sobrescritos. Chaves novas de updates futuros aparecem automaticamente.

---

## **Formatação — MiniMessage**

Os valores são parseados com **[MiniMessage](https://docs.advntr.dev/minimessage/format.html)**. Você pode usar:

| Recurso | Exemplo |
| :--- | :--- |
| Cores nomeadas | `<red>`, `<gold>`, `<light_purple>` |
| Cores hex | `<#ff8800>` |
| Gradientes | `<gradient:#ff0000:#0000ff>Rainbow</gradient>` |
| Decorações | `<bold>`, `<italic>`, `<underlined>`, `<st>` (riscado), `<reset>` |
| Hover | `<hover:show_text:'<yellow>Clique pra copiar!'>...</hover>` |
| Click | `<click:copy_to_clipboard:'valor'>...</click>` |

**Os códigos legados ainda funcionam** como fallback — `&a`, `&l`, `§c` e `&#rrggbb` são convertidos automaticamente antes do parse. Então `&a&lTESTE` renderiza verde e negrito.

Mensagens de chat suportam hover/click de verdade; texto de GUI é desenhado com o renderer legado, então hover/click lá é ignorado, mas cores (inclusive hex) continuam valendo.

---

## **Placeholders**

Alguns valores têm tokens `{nome}` que o mod substitui em runtime, ex:

```json
"commands.give.received": "<green>Você recebeu o cosmético: <white>{item}",
"messages.cosmetic.slot_limit": "<red>[!] Você atingiu o limite de itens no slot {slot} (Limite: {limit})."
```

Mantenha o token escrito exatamente (`{item}`, `{slot}`, `{limit}`, `{id}`, `{player}`, `{value}`, …) — se remover, a substituição só não acontece.

---

## **Exemplo**

```json
// accessories.json
"accessories.category.head": "<gradient:#a855f7:#6d28d9><bold>Cabeça</bold></gradient>",
"accessories.tooltip.fly": " <yellow>✦ <white>Concede Voo"
```

`/gc reload`, reabra o guarda-roupa — a categoria Cabeça renderiza com um gradiente roxo.

---

## **Cliente vs. servidor**

Cliente e servidor leem **cada um a sua própria** pasta `config/GreatCosmetics/lang/` do disco — **não há sync por rede**. Distribua a mesma pasta `lang/` com o seu modpack. Se elas divergirem, a GUI usa a cópia do cliente e o chat usa a do servidor.

---

## **Migrando um `lang.json` antigo**

Builds mais antigas usavam um único `config/GreatCosmetics/lang.json`. No primeiro boot de uma build nova o mod importa os valores que você customizou lá pros novos arquivos divididos (com os nomes de chave novos) e renomeia o arquivo antigo pra `lang.json.migrated`.
