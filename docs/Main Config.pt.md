# **Config Principal**

---

O arquivo **`config/greatcosmetics/mainconfig.conf`** guarda as configurações gerais do servidor: slots virtuais, tipos de acessório, banco de dados, resource pack forçado e comandos de boot. Ele é gerado no primeiro boot e regravado (com as chaves que faltarem preenchidas) toda vez que carrega.

Aplique mudanças com `/gc reload`.

---

## **Template Padrão**

```json
{
  "autoDetectModels": true,
  "devModePermission": "gc.perm.devmode",
  "tagGroupBlacklist": ["default"],

  "useMySQL": false,
  "mysqlHost": "localhost",
  "mysqlPort": 3306,
  "mysqlDatabase": "greatcosmetics",
  "mysqlUser": "root",
  "mysqlPassword": "password",

  "slots": {
    "HEAD":  { "defaultLimit": 1, "permission": "gc.slot.head" },
    "FACE":  { "defaultLimit": 1, "permission": "gc.slot.face" },
    "NECK":  { "defaultLimit": 1, "permission": "gc.slot.neck" },
    "CHEST": { "defaultLimit": 1, "permission": "gc.slot.chest" },
    "BACK":  { "defaultLimit": 1, "permission": "gc.slot.back" },
    "WAIST": { "defaultLimit": 1, "permission": "gc.slot.waist" },
    "LEGS":  { "defaultLimit": 1, "permission": "gc.slot.legs" },
    "FEET":  { "defaultLimit": 1, "permission": "gc.slot.feet" },
    "HAND":  { "defaultLimit": 1, "permission": "gc.slot.hand" }
  },

  "types": {
    "necklace": { "slot": "NECK", "limitPerPlayer": 1, "permission": "gc.type.necklace" },
    "scarf":    { "slot": "NECK", "limitPerPlayer": 1, "permission": "gc.type.scarf" }
  },

  "forceTexture": false,
  "textureId": "greatcosmetics",
  "textureUrl": "",
  "textureSha1": "",

  "startupCommands": []
}
```

---

## **Parâmetros**

### **1. Modelos**

* **`autoDetectModels`** *(padrão `true`)* — deixa o mod escanear o resource pack e gerar automaticamente os overrides de Custom Model Data no item fantasma. Deixe ligado a menos que você monte o JSON de modelo do item na mão.

### **2. Dev Mode**

* **`devModePermission`** *(padrão `gc.perm.devmode`)* — o node de permissão que dá o bypass de **Dev Mode** (equipar qualquer cosmético pra teste sem possuir). Mude se quiser outro nome de node.

### **3. Blacklist de Grupos de Tag**

* **`tagGroupBlacklist`** — nomes de grupo do LuckPerms que **nunca** são importados como Tags de chat (sem case-sensitive). Adicione grupos internos/administrativos aqui pra eles não sujarem o menu de Tags. `default` já vem na lista. Ver [Tags](Tags.md).

### **4. Banco de Dados**

* **`useMySQL`** *(padrão `false`)* — `false` usa o arquivo **SQLite** local embutido (`config/greatcosmetics/database.db`). `true` conecta no servidor MySQL abaixo.
* **`mysqlHost` / `mysqlPort` / `mysqlDatabase` / `mysqlUser` / `mysqlPassword`** — dados de conexão, usados só quando `useMySQL` é `true`.

Explicação completa em [Armazenamento (Banco de Dados)](Storage.md).

### **5. Slots**

`slots` mapeia cada um dos nove nomes de slot virtual pra:

* **`defaultLimit`** — quantos cosméticos um jogador normal pode usar nesse slot.
* **`permission`** — o node **base** pro sistema de tiers de limite (`<base>.<N>`, `<base>.bypass`). Ver [Slots & Tipos](Slots and Types.md).

Você pode remover slots que não quer, mas os nove nomes acima são os únicos válidos.

### **6. Tipos**

`types` é um mapa livre — a chave é o nome do tipo que você vai digitar no campo **Type** de um cosmético. Cada tipo tem:

* **`slot`** — informativo; a qual slot virtual esse tipo pertence.
* **`limitPerPlayer`** — máximo de cosméticos desse tipo que um jogador pode usar ao mesmo tempo.
* **`permission`** — node base pros tiers `<base>.<N>` / `<base>.bypass`.

### **7. Resource Pack Forçado**

Em vez de `resource-pack` / `resource-pack-sha1` no `server.properties` (que precisam de restart), o mod pode enviar o pack sozinho:

* **`forceTexture`** *(padrão `false`)* — habilita o envio do pack no join e no `/gc reload`.
* **`textureId`** — qualquer texto; identifica o pack pro cliente (não precisa ser um UUID).
* **`textureUrl`** — um link de **download direto** do `.zip` do pack.
* **`textureSha1`** — deixe em branco; o mod calcula o SHA-1 real automaticamente. Só preencha se você hospeda em algum lugar que exige um valor fixo.

Ver [Resource Pack](Resource Pack.md).

### **8. Comandos de Boot**

* **`startupCommands`** — lista de comandos rodados **como console** alguns segundos depois de o servidor terminar de iniciar (mais tarde que o `SERVER_STARTED`, pra mods/plugins lentos já estarem prontos). Exemplo:

```json
"startupCommands": [ "lp group vip permission set gc.slot.head.3 true" ]
```

A página **Server Config** do Dev Studio edita essa lista dentro do jogo.
