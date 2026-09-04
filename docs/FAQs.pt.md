# **Perguntas Frequentes**

---

## **Dúvidas Comuns**

### **1. Os jogadores abrem `/wardrobe` mas todo cosmético está sumido / quebrado.**

Quase sempre o **resource pack** não está carregado no cliente. O GreatCosmetics já embute modelos e texturas dos cosméticos internos, mas qualquer cosmético que você adicionar precisa de um resource pack no cliente com os arquivos `models/`, `textures/icons/`, `geo/` e `textures/` correspondentes. Ative o [Resource Pack Forçado](Resource Pack.md) ou coloque o pack no modpack.

---

### **2. O servidor diz "sem licença válida" e nada funciona.**

Você está num servidor dedicado sem uma chave ativada. Rode `/gc activation GREATCOSMETICS-XXXX-XXXX`. Se a ativação falhar:

* A chave pode estar vinculada a outro IP (chaves são de servidor único).
* O backend de licença pode estar acordando — a primeira requisição depois de um tempo parado pode levar até um minuto; tente de novo.
* O hash do seu jar pode não estar registrado ainda pra essa release — use uma chave `-DEV-` enquanto isso.

Ver [Licença & Ativação](License.md).

---

### **3. Eu preciso do LuckPerms?**

Não pra rodar o mod, mas é muito recomendado. Sem ele: só operadores usam os subcomandos `/gc` ou o Dev Studio, os tiers de limite por slot/tipo não fazem nada, o gate de permissão por cosmético não pode ser usado, e as **Tags de grupo** aparecem mas nunca aplicam um prefixo de verdade.

---

### **4. Onde eu adiciono meus modelos 3D?**

Coloque os arquivos num resource pack e referencie por nome no Dev Studio. Convenções:

* **Ícone chapado:** `assets/greatcosmetics/textures/icons/<nome>.png`
* **Modelo vanilla:** `assets/greatcosmetics/models/<nome>.json`
* **Modelo GeckoLib:** `geo/item/<nome>.geo.json` + `textures/item/<nome>.png` (+ `animations/item/<nome>.animation.json` opcional) — em **qualquer** namespace.

Ver [Partes & Modelos](Parts and Models.md).

---

### **5. Cosméticos podem dar stats de verdade (armadura, voo, velocidade)?**

Sim. Qualquer cosmético pode dar pontos de armadura, resistência, voo estilo criativo, multiplicadores de velocidade no chão/voo/água, auto-feed e efeitos de poção permanentes. Ver [Atributos & Habilidades](Attributes.md). Também pode carregar bônus de **Lure** do Cobblemon (taxa de shiny, IVs, chance de captura, pesca…) — ver [Sistema de Lure](Lure System.md).

---

### **6. O capacete de diamante real de um jogador virou cosmético. Por quê?**

Você configurou esse item no `armor_cosmetics.json` (ou pelo botão "+ Armor" do Dev Studio). Quando um jogador entra segurando um item real correspondente, o mod remove ele do inventário e desbloqueia a versão cosmética no guarda-roupa. Ver [Cosméticos de Armadura](Armor Cosmetics.md).

---

### **7. Editei um arquivo de config e nada mudou.**

Rode `/gc reload`. Pro `mainconfig.conf` e os arquivos `lang/` isso basta. **Modelos** de cosmético (GeckoLib `.geo`) também precisam do resource pack do cliente estar atualizado — o `/gc reload` reenvia se você usa o Resource Pack Forçado.

---

### **8. Como eu traduzo o mod / mudo as mensagens dele?**

Tudo fica em `config/greatcosmetics/lang/*.json`, um arquivo por área, tudo renderizado com MiniMessage. Edite os valores, `/gc reload`. Ver [Idioma & MiniMessage](Language.md).

---

!!! tip "Ainda travado?"
    Abra um **ticket de suporte** no nosso [Discord](https://discord.gg/aDCgBbvRe5) com o seu `latest.log` e uma descrição do que você esperava.
