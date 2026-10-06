# Origens_BCN
# Origen's BCN · Gestió de pressupostos

Web estàtic per generar propostes de servei en PDF, fer-ne el seguiment i consultar el Google Sheets de serveis.

## Apartats

- **Generar pressupost** (`#generar`): dades del client, dates, professionals, horaris i tarifes. Cada proposta rep una referència aleatòria única (`OBCN-26-7K4Q9`) que surt al PDF, al nom del fitxer i a l'historial.
- **Pressupostos** (`#pressupostos`): historial amb estat (Esborrany, Enviat, Acceptat, Rebutjat, Facturat), data de seguiment, notes, PDF, duplicar i "Copiar fila per a Sheets".
- **Serveis** (`#serveis`): Google Sheets incrustat. La columna *Referència* enllaça cada servei amb la seva proposta.

## Publicar a GitHub Pages

1. Crea un repositori i puja tot el contingut d'aquesta carpeta (amb `index.html` a l'arrel).
2. A *Settings > Pages*, tria la branca `main` i la carpeta `/ (root)`.
3. El web quedarà a `https://<usuari>.github.io/<repositori>/`.

## Codi d'accés

El web demana un codi de 4 xifres en entrar. Un cop introduït, queda desbloquejat fins que es tanca la pestanya o es prem **Bloquejar** al menú. Després de 5 intents fallits, s'espera 30 segons.

Al codi font no hi ha el codi en clar, només el seu hash SHA-256. Per canviar-lo, calcula el hash nou i substitueix `PIN_HASH` a `index.html`:

```
echo -n "origens-bcn:NOUCODI" | shasum -a 256
```

**Important:** és un filtre per evitar visites casuals, no una protecció real. Amb el repositori públic, qualsevol persona amb coneixements tècnics pot llegir els fitxers o provar els 10.000 codis possibles. No pugeu al repositori dades de clients, preus confidencials ni l'enllaç del Google Sheets.

## Configuració

Edita `assets/js/config.js` per canviar tarifes, professionals, tipus de servei, estats, prefix de referència i l'enllaç per defecte del Google Sheets.

## Dades

Els pressupostos es desen al `localStorage` del navegador: cada navegador i dispositiu té el seu propi historial, i esborrar les dades del navegador els elimina. Fes servir **Còpia de seguretat** (JSON) regularment i **Restaurar còpia** per passar-los a un altre ordinador.

## Estructura

```
index.html
assets/css/styles.css
assets/js/config.js       configuració editable
assets/js/logo.js         logo incrustat per al PDF
assets/js/pdf-builder.js  maquetació del PDF (jsPDF + AutoTable)
assets/js/app.js          generador, historial i Sheets
assets/img/logo.jpg
```
