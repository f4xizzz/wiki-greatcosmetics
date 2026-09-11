# **Cosméticos de Armadura**

---

Um **cosmético de armadura** vincula um cosmético do guarda-roupa a um **item real**. Quando um jogador entra segurando esse item em qualquer lugar do inventário, o mod remove o item real e desbloqueia a versão cosmética no guarda-roupa dele.

É assim que você transforma "uma skin de capacete de diamante personalizada" que já existe como item no seu servidor num cosmético de verdade — o jogador mantém o visual, libera o slot de armadura, e pode alternar no guarda-roupa.

Arquivo de catálogo: **`config/GreatCosmetics/armor_cosmetics.json`**.

---

## **Criando um**

Dev Studio → página **Cosmetics** → **+ Armor**. O editor é igual ao de um cosmético normal, exceto:

* O ID **não é editável** (renomear quebraria a chave do mapa).
* Você define um campo **Real Item** — um id de item do Minecraft/mod tipo `minecraft:diamond_helmet` ou `cobblemon_armory:algo`.

Todo o resto — Display Name, Slot, modelo 3D, atributos, efeitos de poção, permissões/tags concedidas, Lure, sons — funciona exatamente como um cosmético padrão, e vale **enquanto o item real está vestido no slot de armadura de verdade** (ele nunca ocupa um slot virtual como os cosméticos normais).

As partes renderizam o **modelo 3D real da armadura** (a mesh de verdade do vanilla/mod, não um ícone chapado), colocado no osso que bate com o **Anchor** de cada parte — ver [Dev Studio → Editando uma parte](Dev Studio.md#editando-uma-parte) pro botão de auto-split que já organiza peitoral/calça/bota nas partes do corpo certas, e o [gizmo 3D](Parts and Models.md#o-gizmo-3d) pra ajustar cada uma.

---

## **Entrada padrão**

Uma instalação nova (sem `armor_cosmetics.json` ainda) gera um exemplo — um **Capacete de Tartaruga**, escolhido justamente por mostrar que armor points/toughness/tooltip *e* efeitos de poção podem vir de um cosmético de armadura:

```json
{
  "convertedItems": {
    "turtle_helmet": {
      "itemId": "minecraft:turtle_helmet",
      "slot": "HEAD",
      "type": "armor_cosmetic",
      "effects": ["minecraft:water_breathing:1"]
    }
  }
}
```

* A chave (`turtle_helmet`) é o id de cosmético usado por `/gc give`, tags, etc.
* `itemId` é o item real que ele representa.
* `effects` concede **Respiração Aquática** enquanto a peça está vestida — ver [Concedendo efeitos de poção](#concedendo-efeitos-de-pocao) abaixo. (Essa entrada só é gerada numa instalação nova; um `armor_cosmetics.json` já existente com o exemplo antigo `diamond_helmet` fica intocado — edite ou apague na mão se quiser o exemplo novo.)

!!! warning "O item precisa existir"
    Se `itemId` aponta pra um item que não está carregado (mod não instalado, erro de digitação), o console imprime um aviso e a entrada é ignorada.

---

## **Concedendo efeitos de poção** {#concedendo-efeitos-de-pocao}

O campo **Special Effects → `>> Select Effects`** de um cosmético de armadura (o mesmo que um cosmético normal usa) funciona aqui também: qualquer efeito de poção listado ali é aplicado enquanto o item real está vestido, e removido no instante em que é tirado.

Isso **não** é o mod lendo um efeito vanilla do item real — é independente do que o item real normalmente faria. O exemplo padrão acima ilustra bem isso: a Respiração Aquática de um Capacete de Tartaruga de verdade é hardcoded pelo Minecraft vanilla especificamente àquele item no slot de cabeça de verdade, não é algo exposto que o mod possa "copiar" — então o cosmético de armadura concede a Respiração Aquática por conta própria, através da própria lista `effects`, enquanto a peça estiver equipada (não só debaixo d'água, diferente do efeito vanilla). Use o mesmo campo pra anexar qualquer efeito de poção a qualquer cosmético de armadura, independente do que o item real normalmente faz.

---

## **Como a conversão funciona**

No join do jogador:

1. O mod escaneia o inventário do jogador por qualquer item real registrado aqui.
2. Ele **remove** o item e chama `unlockCosmetic` pro cosmético correspondente.
3. O jogador recebe uma mensagem no chat ("Sua *X* virou cosmético! …", texto em `lang/messages.json`).
4. A versão cosmética agora aparece no guarda-roupa.

O `/gc give <armor_cosmetic_id>` também funciona — ele desbloqueia o cosmético sem precisar do item físico.

O `/gc giveitem <armor_cosmetic_id>` devolve o **item real** (pra o jogador poder trocar ou dropar).

---

## **Removendo um cosmético de armadura**

Apagar ele no Dev Studio remove do catálogo. Jogadores que já tinham desbloqueado mantêm a entrada do guarda-roupa até você também dar `/gc remove` neles; o mapeamento item-real ↔ cosmético é descartado, então entrar com o item não converte mais.
