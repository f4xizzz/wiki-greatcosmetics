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

Todo o resto — Display Name, Slot, modelo 3D / modelo GeckoLib, atributos, Lure, sons — funciona exatamente como um cosmético padrão.

---

## **Entrada padrão**

```json
{
  "convertedItems": {
    "diamond_helmet": {
      "itemId": "minecraft:diamond_helmet",
      "slot": "HEAD",
      "type": "armor_cosmetic"
    }
  }
}
```

* A chave (`diamond_helmet`) é o id de cosmético usado por `/gc give`, tags, etc.
* `itemId` é o item real que ele representa.

!!! warning "O item precisa existir"
    Se `itemId` aponta pra um item que não está carregado (mod não instalado, erro de digitação), o console imprime um aviso e a entrada é ignorada.

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
