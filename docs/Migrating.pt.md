# **Migração (Legado)**

---

O GreatCosmetics evoluiu de um sistema de cosméticos mais antigo que guardava cosméticos como **itens `carved_pumpkin` com um número `custom_model_data`**. Se o seu servidor usava isso, jogadores ainda podem estar segurando esses itens antigos. O sistema de migração troca eles pelas entradas de cosmético novas automaticamente.

Arquivo de config: **`config/GreatCosmetics/legacy_cosmetic_migration.json`**.

---

## **Como funciona**

O arquivo é um mapa de **número `custom_model_data` antigo → id de cosmético novo**:

```json
{
  "1": "party_hat",
  "42": "cool_scarf",
  "77": "wizard_robe"
}
```

No join (e continuamente), o mod escaneia o inventário do jogador. Quando acha uma `carved_pumpkin` com `custom_model_data: 42`, ele:

1. Remove o item antigo.
2. Desbloqueia e equipa o cosmético `cool_scarf` pro jogador.
3. Manda uma mensagem no chat ("Seu cosmético antigo foi migrado automaticamente para: …", texto em `lang/messages.json`).

---

## **Configurando**

1. Liste cada número de CMD antigo e o id de cosmético novo que ele deve virar. O cosmético novo precisa **já existir** no catálogo (crie ele no [Dev Studio](Dev Studio.md) primeiro).
2. `/gc reload`.

!!! warning "Alvo faltando"
    Se um mapeamento aponta pra um id de cosmético que ainda não existe, o mod loga um aviso e **pula** aquele item (ele não é removido) até você criar o cosmético ou corrigir o id. Nada é perdido.

---

## **Migrando do arquivo `lang.json`**

Sem relação com a migração de item: builds mais antigas guardavam todo texto num único `config/GreatCosmetics/lang.json`. A build atual importa automaticamente os seus valores customizados pros novos arquivos divididos `lang/*.json` e renomeia o arquivo antigo pra `lang.json.migrated`. Ver [Idioma & MiniMessage](Language.md).

---

## **Migrando o banco de dados**

Pra mover dados de jogador entre SQLite e MySQL, ver [Armazenamento → Migrando](Storage.md#migrando-sqlite--mysql).
