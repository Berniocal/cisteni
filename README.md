# Hlídač blokového čištění – verze s více upozorněními

## Co se změnilo

Formulář už neposílá jedno číslo, ale více vybraných upozornění najednou.

Například:

```text
14,7,3,2,1,0
```

To znamená:

- 14 dní předem
- 7 dní předem
- 3 dny předem
- 2 dny předem
- 1 den předem
- v den čištění

---

## Tabulka

List se jmenuje:

```text
Sledování
```

Hlavičky:

| email | ulice | upozorneni | posledniOdeslano | aktivni |

Sloupec `upozorneni` obsahuje například:

```text
14,7,3,2,1,0
```

Sloupec `posledniOdeslano` si skript vyplňuje sám, aby neposlal stejný e-mail opakovaně.

---

## Co musíš doplnit

### 1) V `Code.gs`

```js
const SPREADSHEET_ID = "SEM_VLOZ_ID_GOOGLE_TABULKY";
```

### 2) V `index.html`

```js
const SCRIPT_URL = "SEM_VLOZ_URL_APPS_SCRIPT_WEB_APP";
```

---

## Apps Script nasazení

V Apps Scriptu:

**Nasadit → Nové nasazení → Webová aplikace**

Nastav:

- **Spustit jako:** Já
- **Kdo má přístup:** Kdokoli

Pak zkopíruj URL končící `/exec` a vlož ji do `index.html`.

---

## Drive API

V Apps Scriptu zapni:

**Služby → + → Drive API → Přidat**

Je to nutné kvůli převodu PDF na Google dokument.

---

## Denní spouštěč

V Apps Scriptu:

**Spouštěče → Přidat spouštěč**

Nastav:

- funkce: `kontrolaBlokovehoCisteni`
- časový spouštěč
- každý den
- třeba 6:00–7:00

Upozornění `0` znamená e-mail ráno v den čištění, podle času spuštění triggeru.

---

## Důležité

Upozornění „1 hodinu předem“ jsem tam nedal, protože PDF obvykle neobsahuje přesný čas čištění a Apps Script časové spouštěče nejsou přesné na minuty. Spolehlivější je upozornění ráno v den čištění.
