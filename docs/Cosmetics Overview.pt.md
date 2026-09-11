# **Visão Geral dos Cosméticos**

---

Um **cosmético** é uma entrada vestível no catálogo. Ele ocupa um slot virtual, renderiza uma ou mais **partes** 3D no jogador, e pode carregar stats, habilidades, efeitos, bônus de Lure e sons.

O catálogo fica em **`config/GreatCosmetics/cosmeticsconfig.conf`** (JSON apesar da extensão). Você raramente edita na mão — o [Dev Studio](Dev Studio.md) grava pra você e transmite as mudanças ao vivo. Esta página explica o que cada campo significa.

---

## **Anatomia de um cosmético**

| Campo | Significado |
| :--- | :--- |
| **id** (chave do mapa) | Identificador único. Usado por `/gc give`, tags, equipar em NPC, e pra achar os arquivos de modelo. |
| **DisplayName** | Nome MiniMessage mostrado nos menus e no item físico. Vazio → o id capitalizado. |
| **slot** | Um de `HEAD, FACE, NECK, CHEST, BACK, WAIST, LEGS, FEET, HAND`. Controla em qual categoria aparece e qual [limite de slot](Slots and Types.md) se aplica. |
| **type** | Nome de tipo livre (ex: `necklace`). Precisa bater com uma chave no `mainconfig.conf` → `types` pra um limite de tipo valer. `default` = sem limite de tipo. |
| **permission** | Se definido, só jogadores com esse node (ou que desbloquearam) veem e equipam o cosmético. Vazio = disponível pra todo mundo que desbloqueou. |
| **iconId** | Opcional. Nome de um `textures/icons/*.png` diferente pra usar como ícone chapado, assim vários cosméticos podem compartilhar um arquivo de ícone. Vazio = usa o id. |
| **cmd** | O número de Custom Model Data que o mod atribui ao ícone chapado. Gerenciado automaticamente — não defina na mão. |
| **maxDurability** | Se > 0, o item físico mostra uma barra de durabilidade (puramente visual). |
| **tooltipDescription** | Linhas opcionais em MiniMessage (separadas por `\n`) mostradas abaixo do Display Name no guarda-roupa. Vazio = nada a mais. |
| **grantedPermissions** / **minecraftTags** | Separadas por vírgula no editor. Aplicadas ao jogador enquanto o cosmético está equipado e o gate `permission` passa; removidas ao desequipar. Ver [Permissões](Permissions.md). |
| **unlockPermission** / **unlockTag** | Se definido, qualquer jogador com esse node ou scoreboard tag ganha o cosmético automaticamente — sem linha no banco, sem `/gc give`. Perdido no instante em que deixa de qualificar. Ver [Permissões § Auto-Unlock](Permissions.md#auto-unlock). |
| **variants** | Posicionamentos alternativos opcionais do mesmo model, cada um escolhível separadamente no guarda-roupa. Ver [Dev Studio § Variants](Dev Studio.md#variants). |
| **parts** | A lista de peças 3D — ver [Partes & Modelos](Parts and Models.md). |

Mais os sistemas opcionais: **armor / toughness**, **EnableFly + multiplicadores de velocidade**, **AutoFeed**, **effects** (poção — também funciona em [cosmético de armadura](Armor Cosmetics.md)), **effectVisual / flyParticle / shiftParticle**, **isBackpack**, **lure**, **sounds** — cada um tem a sua página.

!!! warning "O mod em si não tem conteúdo de cosmético"
    O GreatCosmetics é o framework, não um pacote de models. Um `cosmeticsconfig.conf` novo **não tem nenhum cosmético virtual de exemplo**, e os poucos exemplos pequenos que o mod *inclui* (um cosmético de armadura — ver [Cosméticos de Armadura](Armor Cosmetics.md) — mais algumas models de teste chapadas/GeckoLib) podem ficar e ser usados no seu servidor numa boa, mas não são pra serem o seu conteúdo de verdade. **Os cosméticos mostrados no vídeo de showcase do mod não vêm junto com o mod** — você precisa trazer suas próprias models (feitas por você seguindo o padrão abaixo e [Criando Modelos](Making Models.md), compradas — ou em breve compráveis — no Discord oficial da SaSDevelopment, de qualquer outro lugar, ou reaproveitadas de armadura de outro mod). Ainda travado depois de ler a documentação? Entra no [Discord](https://discord.gg/GbbbNvQG3N) e pergunta.

---

## **Como um jogador ganha um cosmético**

| Método | Resultado |
| :--- | :--- |
| `/gc give <id> [jogador]` | Desbloqueia no guarda-roupa. |
| `/gc giveitem <id> [jogador]` | Dá o item físico; o jogador ainda equipa pelo guarda-roupa. |
| Segurar um item real correspondente no join | Convertido automaticamente (ver [Cosméticos de Armadura](Armor Cosmetics.md)). |
| Ter o node `permission` | Aparece automaticamente, sem precisar de `/gc give`. |
| Operador / **Dev Mode** | Todo cosmético aparece como possuído. |

---

## **Exemplo mínimo**

```json
"party_hat": {
  "DisplayName": "<light_purple>Chapéu de Festa",
  "slot": "HEAD",
  "type": "default",
  "permission": "",
  "parts": [
    { "customModelData_or_ID": "party_hat", "anchor": "HEAD" }
  ]
}
```

Com `assets/greatcosmetics/textures/icons/party_hat.png` no resource pack, `/gc give party_hat <jogador>` e ele aparece na categoria **Cabeça** do guarda-roupa.
