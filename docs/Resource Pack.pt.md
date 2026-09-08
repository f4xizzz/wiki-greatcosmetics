# **Resource Pack**

---

Os cosméticos que vêm com o mod têm os modelos e texturas **dentro do jar**. Qualquer coisa que você adicionar fica num **resource pack** que precisa chegar no cliente.

---

## **O que vai no pack**

Tudo sob `assets/greatcosmetics/` salvo indicado:

| Caminho | Uso |
| :--- | :--- |
| `textures/icons/<nome>.png` | Ícone chapado estilo inventário (16×16 ou maior). O caso mais comum. |
| `models/<nome>.json` | Um modelo de item vanilla (opcional — só se você quer um modelo vanilla chapado/3D personalizado em vez de um ícone simples). |
| `geo/item/<nome>.geo.json` | Um arquivo de geometria **GeckoLib** — em **qualquer** namespace, não só `greatcosmetics`. |
| `textures/item/<nome>.png` | A textura desse modelo GeckoLib — qualquer namespace. |
| `animations/item/<nome>.animation.json` | Animação GeckoLib opcional — qualquer namespace. |

O **nome** é o que você digita no campo de parte do cosmético no [Dev Studio](Parts and Models.md). Com o modo **Caminho Exato** ligado, o campo vira um caminho relativo completo (`pasta/nome`) resolvido em qualquer namespace.

O `autoDetectModels` no `mainconfig.conf` (ligado por padrão) deixa o mod escanear o pack e montar os overrides de Custom Model Data pra você.

---

## **Levando o pack aos clientes**

### Opção A — Modpack

Coloque o resource pack no seu modpack / server pack. É o mais simples se você controla a instalação do cliente.

### Opção B — Resource Pack Forçado (recomendado)

Deixe o mod enviar o pack no join e no `/gc reload`. No [`mainconfig.conf`](Main Config.md):

```json
"forceTexture": true,
"textureId": "greatcosmetics",
"textureUrl": "https://seu-host.exemplo/greatcosmetics-pack.zip",
"textureSha1": ""
```

* **`textureUrl`** tem que ser um **download direto** do `.zip` (Dropbox `?dl=1`, um asset de release do GitHub, seu próprio servidor web…). Links de compartilhamento do Google Drive **não** funcionam.
* Deixe o **`textureSha1`** vazio — o mod baixa o arquivo, calcula o SHA-1 real e faz cache. Ele recheca no `/gc reload` e reenvia se o arquivo mudou.
* **`textureId`** é qualquer rótulo; ele só precisa mudar se você quer que os clientes tratem como um pack diferente.

!!! note "Só um pack forçado"
    O Minecraft aplica um resource pack de servidor por vez. Se o seu servidor já força um pack via `server.properties` ou outro mod, junte os assets do GreatCosmetics nesse pack em vez de usar o `forceTexture`.

---

## **Resolução de Problemas**

* **Tudo é uma textura roxa/preta de faltando** → o cliente não tem pack, ou o pack falhou ao baixar. Cheque o `latest.log` do cliente por um erro de download de resource pack.
* **Um cosmético fica genérico enquanto os outros estão certos** → o `models/<id>.json` ou o `textures/icons/<id>.png` desse cosmético está faltando. O console imprime um `WARNING` nomeando o arquivo esperado.
* **Modelo GeckoLib invisível** → o `geo/item/<nome>.geo.json` **ou** o `textures/item/<nome>.png` está faltando; o console imprime qual.
* Sempre `/gc reload` depois de mudar o pack pra o SHA-1 do pack forçado atualizar.
