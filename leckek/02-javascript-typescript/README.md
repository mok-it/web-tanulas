# 02. JavaScript és TypeScript

## Mit fogsz csinálni?

Az előző leckében megépített oldal mozdulatlan: a hat feladatkártya kézzel be van írva a
HTML-be. Most ezt megfordítjuk. Lesz egy **adatszerkezet** a feladatokról, és a kártyákat
onnan rajzoljuk ki kódból. Ha ez megvan, szinte ingyen jön a többi: kereső és
találatszámláló.

A következőket fogod használni:

1. [**JavaScript**](https://developer.mozilla.org/en-US/docs/Web/JavaScript): a nyelv, ami a böngészőben fut
2. [**DOM**](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction): ezen keresztül nyúl a kód az oldalhoz
3. [**TypeScript**](https://www.typescriptlang.org/): ugyanaz a kód, csak típusokkal

## Mire lesz szükséged?

- [VS Code](https://code.visualstudio.com/)
- [Bun](https://bun.sh/) telepítve, lásd a [SETUP.md](../../SETUP.md)-t
- Az `1-start/` mappa, amiben az előző lecke végeredménye van

---

## 1. Az első sor JavaScript

Nyisd meg VS Code-ban az `1-start/index.html` fájlt. Ez az előző lecke kész oldala.

Hozz létre mellé egy új fájlt: `app.js`. Ennyi legyen benne:

```js
console.log("Hello világ!");
```

Az `index.html`-ben szúrd be ezt a sort közvetlenül a záró `</body>` tag **elé**:

```html
<script src="app.js"></script>
```

Az előző leckében a Live Server szolgálta ki az oldalt. Ebben a leckében a
[Bun](https://bun.sh/) teszi, mert a végén ő fogja a TypeScriptet is lefordítani. Nyiss egy
terminált a VS Code-ban (a menüben **Terminal** > **New Terminal**), és nézd meg, hogy
megvan-e:

```
bun --version
```

Ha nem ismeri a parancsot, telepítsd a [SETUP.md](../../SETUP.md) szerint. Ha megvan, lépj
be az `1-start` mappába, és indítsd el az oldalt:

```
cd leckek/02-javascript-typescript/1-start
bun index.html
```

A `cd` sor a repó gyökeréből indul. Ha a VS Code-ban a repó mappáját nyitottad meg, a
terminál alapból ott áll.

Kiírja, hol fut az oldal, például `http://localhost:3000/`. Nyisd meg a böngészőben, és nyomj
`F12`-t. A megnyíló eszköztárban válaszd a **Console** fület. Ha látod, hogy "Hello világ!",
akkor sikerült az `app.js` szkriptet futtatni.

A `console.log` az első és legfontosabb eszközöd: bármit kiírhatsz vele, és megnézheted, mi
van egy változóban. Nem a felhasználónak szól, hanem neked.

Két dolgot érdemes rögtön megjegyezni:

- A `script` tag azért van a `body` **végén**, mert a böngésző fentről lefelé olvas. Mire
  idáig ér, a fenti elemek már léteznek, és a kód hozzájuk tud nyúlni. Ha a `head`-be
  raknánk, még semmi sem lenne kész. A Bun ezt a sort kiszolgáláskor átírja egy modulra
  (module), ami amúgy is megvárja az oldalt, ezért az **Elements** fülön a `head`-ben fogod
  látni. Te mégis a `body` végére írd, mert nem minden oldalt a Bun szolgál ki.
- Az oldal **magától frissül**, amikor elmentesz egy fájlt, akár az `index.html`-t, akár az
  `app.js`-t. A terminált hagyd futni, amíg dolgozol. Ha leállítanád, `Ctrl` + `C`.

A konzolban a Bun is megszólal, a `[Bun]` kezdetű sorok tőle jönnek, nem a te kódodtól.
Ha egyszer olyan hibát ír, ami akkor sem tűnik el, amikor a kódod már biztosan jó (például
egyszerre mentettél el két fájlt), állítsd le a szervert, és indítsd újra a
`bun index.html`-lel.

## 2. A nyelv dióhéjban

A konzol, amit az előbb megnyitottál, egy teljes értékű játszótér: bármit beírhatsz,
`Enter`, és kiírja az eredményt. Próbáld ki mindegyik példát ott.

> Ha bemásolsz valamit, a Chrome elsőre letilthatja a beillesztést, és arra kér, hogy írd be:
> `allow pasting`. Ez védelem a csalók ellen, akik idegen kódot próbálnak a konzolba
> beilleszttetni veled. Itt nyugodtan engedélyezd, vagy gépeld be a példákat kézzel.

### Változók

```js
const siteName = "Feladatbank";
let count = 6;
count = 7;
```

`const`: nem lehet újra értéket adni neki. `let`: lehet. Használj `const`-ot, amíg nem
derül ki, hogy `let` kell. Van egy harmadik, a `var`: ezzel ne foglalkozz, régi, és van
néhány meglepő tulajdonsága.

> A `const` arra vonatkozik, hogy a **változó** nem mutathat másik értékre. Ha az érték egy
> objektum vagy tömb, annak a **tartalma** attól még változhat: a `const arr = [1, 2]`
> után az `arr.push(3)` működik, az `arr = [4]` nem.

### Primitív típusok

Az 5 legfontosabb primitív típus:

| Típus       | Példa              | Mire való                    |
| ----------- | ------------------ | ---------------------------- |
| `string`    | `"Hamis érme"`     | szöveg                       |
| `number`    | `12`, `3.14`, `-1` | minden szám                  |
| `boolean`   | `true`, `false`    | igaz vagy hamis              |
| `undefined` | `undefined`        | a változó nem kapott értéket |
| `null`      | `null`             | szándékosan üres             |

Amit érdemes kiemelni belőle:

- Nincs külön egész és lebegőpontos típus, a `number` mindkettő, és mindig lebegőpontosan
  tárolódik.
- **Az `undefined` és a `null` nem ugyanaz.** `undefined`: nincs értéke. `null`: van értéke,
  és az a "semmi". Mindkettővel fogsz találkozni.
- **Ami nem primitív, az objektum.** A tömb, a függvény és a dátum is objektum. A primitív
  értékek másolódnak, az objektumok hivatkozásként (reference) adódnak tovább: ha egy tömböt
  két változóba teszel, mindkettő ugyanazt az egy tömböt látja.

A `typeof` operátorral bármiről megkérdezheted, micsoda:

```js
typeof "Hamis érme"; // "string"
typeof 12; // "number"
typeof [1, 2, 3]; // "object"
typeof function () {}; // "function"
typeof null; // "object"
```

> Az utolsó sor egy hiba a nyelvben, ami 1995 óta benne van. A `null` nem objektum, de a
> `typeof` azt mondja. Soha nem javították, mert túl sok létező oldal épül rá.

### Sztringek

A backtick idézőjel (`` ` ``, magyar billentyűzeten `AltGr` + `7`, és ha nem jelenik meg
rögtön, nyomj utána egy szóközt) különleges: bele lehet írni kifejezéseket `${...}` között,
és több soros is lehet.

```js
const topic = "Kombinatorika";
console.log(`A témakör: ${topic}`);
```

Szövegek összerakására használjuk majd, például a találatszámláló feliratához.

A sztringeknek sok beépített metódusa van. Ezek a fontosabbak, a `const s = "Hamis érme";`
sorral a hátunk mögött:

| Metódus                        | Eredmény            | Mit csinál                                                 |
| ------------------------------ | ------------------- | ---------------------------------------------------------- |
| `s.length`                     | `10`                | hossz, ez nem metódus, hanem tulajdonság (property)        |
| `s.toLowerCase()`              | `"hamis érme"`      | csupa kisbetű, `toUpperCase` a párja                       |
| `s.includes("érme")`           | `true`              | benne van-e a részlet                                      |
| `s.startsWith("Hamis")`        | `true`              | ezzel kezdődik-e, `endsWith` a párja                       |
| `s.indexOf("érme")`            | `6`                 | hányadik karaktertől, vagy `-1`                            |
| `s.slice(0, 5)`                | `"Hamis"`           | részlet a megadott intervallumon, nem beleszámítva a végét |
| `s.slice(-4)`                  | `"érme"`            | negatív index a végétől számol                             |
| `s.replace("Hamis", "Valódi")` | `"Valódi érme"`     | csere, `replaceAll` az összesre                            |
| `"  Hamis érme  ".trim()`      | `"Hamis érme"`      | szóközök eltakarítása a két végéről                        |
| `s.split(" ")`                 | `["Hamis", "érme"]` | felvágás tömbbé az elválasztó mentén                       |
| `s[0]`                         | `"H"`               | egy karakter, indexeléssel                                 |

Két dolgot jegyezz meg:

- **Egyik sem változtatja meg az eredetit.** A sztring **megváltoztathatatlan**
  (immutable): minden metódus új sztringet ad vissza. Ha `s.toUpperCase()`-t írsz, de nem
  teszed el az eredményt, nem történt semmi.
- A `toLowerCase` és az `includes` párosa lesz a keresőnk motorja a 8. fejezetben.

### Függvények

```js
function double(x) {
  return x * 2;
}

const double2 = (x) => x * 2;
```

A kettő ugyanazt csinálja. A második a **nyílfüggvény** (arrow function): rövid alak, és ha
egyetlen kifejezésből áll, a `return` is elhagyható. Leginkább ott használjuk, ahol egy
függvényt adunk át egy másik függvénynek, és nincs értelme külön nevet adni neki.

### Objektumok

```js
const task = {
  title: "Hamis érme",
  difficulty: "medium",
};

task.title; // "Hamis érme"
task.difficulty; // "medium"
```

Kulcs-érték párok. Nem kell hozzá osztály vagy konstruktor, csak leírod.

### Tömbök

Három gyakori metódus, az első kettőt a leckében végig használni fogjuk:

```js
const numbers = [1, 2, 3, 4, 5];

numbers.map((x) => x * x); // [1, 4, 9, 16, 25]
numbers.filter((x) => x % 2 === 0); // [2, 4]
["a", "b", "c"].join(" - "); // "a - b - c"
```

- `map`: minden elemre lefuttatja a függvényt, és az eredményekből **új tömböt** csinál.
  Ugyanannyi elemű, mint az eredeti.
- `filter`: megtartja azokat az elemeket, amikre a függvény igazat adott. Rövidebb tömb.
- `join`: sztringek tömbjéből egy darab sztring, a megadott elválasztóval.

Egyik sem írja át az eredeti tömböt, mindegyik újat ad vissza. Ezért lehet őket láncolni:
`numbers.filter(...).map(...)`.

> Egyenlőséget mindig `===`-szel vizsgálj, ne `==`-vel. A `==` előbb átalakítja az
> operandusokat közös típusra, és ebből furcsaságok jönnek ki: a `"" == 0` igaz, a
> `"" === 0` hamis. A `!==` ugyanígy a `!=` helyett.

## 3. A DOM

Amikor a böngésző beolvassa a HTML fájlt, csinál belőle egy **objektumfát** a memóriában.
Ezt hívjuk DOM-nak (Document Object Model). Amit az oldalon látsz, az a DOM, nem a fájl.

Írd be a konzolba:

```js
document.querySelector("h1");
```

Visszaadja az első `h1` elemet. A `querySelector` ugyanazokat a selectorokat érti, amiket a
CSS-ben tanultál: `.card`, `#list`, `article > h3`, bármelyiket. A `querySelectorAll`
pedig nem az elsőt adja vissza, hanem az összes találatot.

Most írd be ezt:

```js
document.querySelector("h1").textContent = "Feladatgyűjtemény";
```

A cím megváltozott az oldalon. Nézd meg az `index.html` fájlt: **nem változott semmi**. És
ha frissíted az oldalt, visszaáll az eredeti.

A leggyakoribb műveletek:

| Kód                                | Mit csinál                                                |
| ---------------------------------- | --------------------------------------------------------- |
| `document.querySelector(sel)`      | Megkeresi az első illeszkedő elemet                       |
| `el.textContent`                   | Az elem szövege, HTML nélkül                              |
| `el.classList.add("bg-white")`     | Osztályt ad hozzá, `remove`, `toggle` és `replace` is van |
| `document.createElement("button")` | Új elemet gyárt, ami még nincs sehol                      |
| `parent.append(child)`             | Beteszi az elemet egy másik elem végére                   |
| `parent.replaceChildren(...)`      | Kicseréli az elem összes gyerekét                         |
| `el.cloneNode(true)`               | Lemásolja az elemet mindenestül                           |

Próbáld ki a konzolban:

```js
document.querySelector("header").classList.add("bg-sky-100");
```

Nem történt semmi. Pedig az osztály rákerült: nézd meg az **Elements** fülön, ott van a
`header`-en. A gond az, hogy a fejlécen már van egy `bg-white`, és most két osztály állítja
ugyanazt a háttérszínt. Hogy melyik nyer, azt **nem** az dönti el, milyen sorrendben vannak
a `class` attribútumban, hanem hogy melyik szabály áll később a CSS-ben. A Tailwind a
`bg-white`-ot rakja hátrébb, így az nyer.

Ezért a régit le kell venni, mielőtt az újat felteszed. Erre van egy külön metódus:

```js
document.querySelector("header").classList.replace("bg-white", "bg-sky-100");
```

A fejléc világoskék lett. Figyeld meg, hogy a Tailwind ehhez is legyártotta a CSS-t, pedig
a `bg-sky-100` osztály sehol nincs benne a HTML fájlban. A böngészőbe húzott Tailwind
figyeli a DOM-ot, és amint megjelenik benne egy új osztály, legyártja hozzá a CSS-t. Ez
nekünk most jól jön, mert a kártyákat kódból fogjuk beszúrni.

## 4. Az adat

Eddig a feladatok szövege a HTML-ben volt. Tegyük át kódba.

Egy feladat így fog kinézni:

```js
{
  title: "Sakktábla lefedése",
  topic: "Kombinatorika",
  difficulty: "easy",
  description: "Egy 8×8-as sakktábláról levágunk két átellenes sarokmezőt...",
}
```

Négy mező, mindegyik az, amit a kártyán látsz. Egy kivétellel: a nehézségnél nem a kiírt
szöveg áll, hanem egy angol kód (`easy`, `medium`, `hard`). A kódban a mezőnevek és az
ilyen azonosító értékek angolul vannak, a magyar felirat csak a kártyára kerül.

Most jöjjön mind a hat, egy tömbben. Töröld ki az `app.js` tartalmát, és írd bele ezt:

```js
const tasks = [
  {
    title: "Sakktábla lefedése",
    topic: "Kombinatorika",
    difficulty: "easy",
    description:
      "Egy 8×8-as sakktábláról levágunk két átellenes sarokmezőt. Lefedhető-e a maradék 62 mező 31 darab 1×2-es dominóval?",
  },
  {
    title: "Hamis érme",
    topic: "Logika",
    difficulty: "medium",
    description:
      "Adott 12 egyforma érme, köztük egy hamis, ami a többinél könnyebb vagy nehezebb. Találd meg három mérlegeléssel egy kétkarú mérlegen!",
  },
  {
    title: "Végtelen sok prím",
    topic: "Számelmélet",
    difficulty: "medium",
    description:
      "Bizonyítsd be, hogy végtelen sok prímszám van! A bizonyítás Eukleidésztől származik, és elfér néhány sorban.",
  },
  {
    title: "Königsbergi hidak",
    topic: "Gráfelmélet",
    difficulty: "easy",
    description:
      "Königsberg városát hét híd köti össze. Bejárható-e úgy a város, hogy minden hídon pontosan egyszer megyünk át?",
  },
  {
    title: "Skatulyaelv a bulin",
    topic: "Kombinatorika",
    difficulty: "medium",
    description:
      "Egy hatfős társaságban bárki bárkit vagy ismer, vagy nem. Bizonyítsd be, hogy mindig van három ember, akik páronként ismerik egymást, vagy három, akik páronként nem!",
  },
  {
    title: "Hilbert szállodája",
    topic: "Halmazelmélet",
    difficulty: "hard",
    description:
      "A szállodában végtelen sok szoba van, és mind foglalt. Érkezik egy új vendég. Hogyan szállásolod el? És ha végtelen sokan érkeznek egyszerre?",
  },
];
```

Ez semmit nem csinál még, csak ott van. Hogy lásd, írd az `app.js` végére:

```js
console.log(tasks.length);
console.log(tasks[0].title);
console.log(tasks.map((task) => task.topic));
```

Mentsd el, és nézd meg a konzolt: `6`, `Sakktábla lefedése`, és egy hatelemű tömb a
témakörökkel. Ha megvan, töröld ki ezt a három sort.

> Miért nem elég beírni a konzolba, hogy `tasks`? A Bun az `app.js`-t **modulként** (module)
> tölti be, és egy modul változói nem látszanak kívülről, a konzolból sem. Ha valamit meg
> akarsz nézni a kódodból, írd ki `console.log`-gal.

## 5. A sablon és az első kártya

Most jön a lényeg: hogyan csinálunk egy adatból egy elemet az oldalon.

A válasz kétlépcsős: **a HTML maradjon HTML-ben, a JavaScript meg töltse ki.**

A `<template>` elem pont erre való. A böngésző beolvassa és értelmezi a tartalmát, de nem
jeleníti meg, és nem is része az oldalnak. Egy minta, amit lemásolhatsz.

Az `index.html`-ben, közvetlenül a `<script>` sor **elé**, tedd be ezt:

```html
<template id="card-template">
  <article
    class="rounded-lg border border-slate-200 bg-white p-5 shadow-sm transition hover:shadow-md"
  >
    <h3 class="mb-2 text-lg font-semibold" data-title></h3>
    <div class="mb-3 flex flex-wrap gap-2">
      <span
        class="rounded-full bg-slate-100 px-2.5 py-0.5 text-xs text-slate-700"
        data-topic
      ></span>
      <span
        class="rounded-full bg-slate-100 px-2.5 py-0.5 text-xs text-slate-700"
        data-difficulty
      ></span>
    </div>
    <p class="text-sm leading-relaxed text-slate-600" data-description></p>
  </article>
</template>
```

Ez ugyanaz a kártya, amit az előző leckében megírtál, két különbséggel: a szövegek helye
üres, és minden kitöltendő elem kapott egy `data-` attribútumot.

A `data-` előtaggal kezdődő attribútumokat a böngésző nem értelmezi, a tiéd. Most arra
használjuk őket, hogy a JavaScript megtalálja a helyet, ahova írnia kell. Lehetne osztállyal
is, de akkor összekeveredne a kinézet a fogódzóval: az osztályok a stílusé, a `data-`
attribútumok a kódé.

Most töröld ki mind a hat `<article>` elemet a rácsot adó `div` belsejéből, és adj a
`div`-nek egy `id`-t:

```html
<div id="list" class="grid gap-4 sm:grid-cols-2 lg:grid-cols-3"></div>
```

Az oldal közepe üres. A kártya nem veszett el, csak átköltözött a sablonba.

Jöjjön a függvény, ami egy feladatból kártyát csinál. Írd az `app.js` végére:

```js
const template = document.querySelector("#card-template");

function card(task) {
  const node = template.content.cloneNode(true);

  node.querySelector("[data-title]").textContent = task.title;
  node.querySelector("[data-topic]").textContent = task.topic;
  node.querySelector("[data-description]").textContent = task.description;
  node.querySelector("[data-difficulty]").textContent = task.difficulty;

  return node;
}
```

Sorról sorra:

- `template.content`: a sablon tartalma. Nem maga a `template` elem, hanem ami benne van.
- `cloneNode(true)`: lemásolja. A `true` azt jelenti, hogy mindenestül, a gyerekeivel
  együtt. `false` esetén csak egy üres burkot kapnál, a tartalma nélkül.
- `[data-title]` egy **attribútum selector**: olyan elemet keres, amin van ilyen nevű
  attribútum. Ugyanúgy működik CSS-ben is.
- `textContent`: a szöveget **szövegként** írja be. Ha egy címben `<` van, az `<` marad, nem
  lesz belőle címke. Ezért nem tud elromlani az oldal az adattól. Van egy testvére, az
  `innerHTML`, ami HTML-ként értelmezi a szöveget: adatot soha ne írj be vele.
- A `querySelector` itt nem a `document`-en fut, hanem a klónon. Így csak azon belül keres,
  és nem találja el véletlenül az oldal egy másik elemét.

Most tedd ki az oldalra. Az `app.js` végére:

```js
const list = document.querySelector("#list");

const firstCard = card(tasks[0]);

list.append(firstCard);
```

Megjelent egy kártya. Majdnem ugyanaz, mint az előző leckében, de most az adatból született.
A nehézség címkéjén egyelőre `easy` áll, ezt a 7. fejezetben rendbe tesszük.

> A klón, amit a `cloneNode` a sablon tartalmából ad, egy **töredék** (DocumentFragment):
> egy zsák, amiben ott vannak az elemek, de maga a zsák nem lesz része az oldalnak. Amikor
> `append`-eled, a tartalma kerül be, a zsák pedig kiürül. Ezért egy klónt csak egyszer
> tudsz beszúrni, minden kártyához új kell.

## 6. Mind a hat

Egy kártya megvan, kell még öt. Ezt két lépésben csináljuk: előbb legyártjuk az összes
kártyát, aztán kitesszük őket az oldalra.

Töröld ki az utolsó két sort (a `firstCard`-osat és az `append`-eset), és írd a helyükre
ezt:

```js
const cards = tasks.map(card);
console.log(cards);
```

Mentsd el, és nézd meg a konzolt. Egy hatelemű tömb, minden eleme egy `DocumentFragment`.
Az oldalon viszont nincs egy kártya se: a töredékek elkészültek, de még nem tettük ki őket.

A `map` minden feladatra lefuttatja a `card` függvényt, és az eredményekből új tömböt
csinál. Figyeld meg, hogy a függvény **nevét** adtuk át, nem hívtuk meg (`card`, nem
`card()`). A `map` fogja meghívni, minden elemre egyszer.

Most töröld ki a `console.log` sort, és írd a helyére:

```js
list.replaceChildren(...cards);
```

Megjelent az összes kártya.

- `replaceChildren`: kicseréli az elem **összes** gyerekét a megadottakra. Ha üresen hívod,
  egyszerűen kitakarítja.
- `...`: a **szétterítő** (spread) operátor. A `replaceChildren` nem tömböt vár, hanem
  akárhány elemet egymás után, vesszővel elválasztva. A `...cards` pont ezt csinálja: a
  tömböt szétbontja, mintha egyenként írtad volna be őket: `cards[0], cards[1], ...`.

**Próbáld ki:** írj be egy hetedik feladatot a tömb végére. Utána nyugodtan bent maradhat.

## 7. A nehézség címkéje

Az előző leckében a nehézség címkéje színes volt: zöld a könnyűnek, sárga a közepesnek,
piros a nehéznek. Most két baj is van vele: mind szürke, mert a sablonban egy fix
osztálylista van, és a felirata angol kód (`easy`), nem magyar szöveg.

Egyiket sem írhatjuk a sablonba, mert feladatonként más. Kódból kell ráraknunk, tehát kell
egy **kikereső tábla** (lookup table), ami minden nehézséghez megmondja a feliratot és az
osztályokat. Lehetne `if`-ekkel is, de JavaScriptben erre a legegyszerűbb eszköz maga az
objektum. Írd a `card` függvény **elé**:

```js
const difficulties = {
  easy: { label: "könnyű", classes: ["bg-emerald-100", "text-emerald-800"] },
  medium: { label: "közepes", classes: ["bg-amber-100", "text-amber-800"] },
  hard: { label: "nehéz", classes: ["bg-rose-100", "text-rose-800"] },
};
```

Egy objektum kulcsait nem csak ponttal lehet elérni, hanem szögletes zárójellel is, és ott
egy változó is állhat: a `difficulties[task.difficulty]` kikeresi a feladat nehézségéhez
tartozó bejegyzést. Abban a `label` a felirat, a `classes` az osztálylista.

Előbb vedd ki a sablonból a nehézség címkéjének szürke színét, hogy legyen mit
felülírni. A `data-difficulty`-s `span` helyére (most négy sor) ez az egy kerüljön:

```html
<span class="rounded-full px-2.5 py-0.5 text-xs" data-difficulty></span>
```

Most a `card` függvényben cseréld le a nehézség sorát erre a négyre:

```js
const difficulty = difficulties[task.difficulty];
const badge = node.querySelector("[data-difficulty]");
badge.textContent = difficulty.label;
badge.classList.add(...difficulty.classes);
```

Mentsd el. Magyar lett a felirat, és visszajöttek a színek.

A `classList.add` akárhány osztálynevet elfogad egymás után, ezért terítjük szét a tömböt
itt is. Előnye az `el.className = "..."`-hoz képest, hogy nem törli le a meglévő
osztályokat, hanem hozzáad.

> Figyeld meg, hogy a `difficulties`-ben **teljes osztálynevek** vannak, nem darabokból rakjuk
> össze őket. Csábító lenne valami ilyesmi: `` `bg-${color}-100` ``. Most működne is, mert a
> böngészőbe húzott Tailwind a kész DOM-ot nézi. A rendes, fordítás idejű Tailwind viszont a
> **forráskódodat** olvassa, és ott a `bg-emerald-100` sehol nem szerepelne, tehát nem is
> gyártaná le. Szokd meg most, mert az 5. leckében már a fordítós változatot
> fogjuk használni.

## 8. Keresés

Az `index.html`-ben a `<h2>` alá, a `<div id="list">` **fölé** tedd be ezt:

```html
<input
  id="search"
  type="search"
  placeholder="Keresés a feladatok között..."
  class="mb-4 w-full rounded-lg border border-slate-300 bg-white px-4 py-2 text-sm focus:border-slate-500 focus:outline-none"
/>
```

Van egy keresőmező, ami még nem csinál semmit.

Ahhoz, hogy csináljon, a kirajzolást **többször** kell tudni futtatni. Most ez két sor,
ami egyszer lefut. Csomagoljuk függvénybe: cseréld le az `app.js` utolsó két sorát erre:

```js
function render() {
  const cards = tasks.map(card);
  list.replaceChildren(...cards);
}

render();
```

Az oldal ugyanúgy néz ki, mint előbb. Most kössük rá a keresőt. Először kell egy fogódzó,
ugyanúgy, mint a listához. Írd a `const list` sor alá:

```js
const search = document.querySelector("#search");
```

Aztán a `render();` hívás **elé**:

```js
search.addEventListener("input", render);
```

Az `addEventListener` két dolgot kap: egy **esemény** (event) nevét és egy függvényt. Ettől
kezdve a böngésző minden ilyen eseménynél meghívja a függvényt. Ezért itt is csak a nevét
adod át: az eseménynél nem te hívod meg, hanem a böngésző. Az `"input"` esemény akkor sül
el, amikor változik a mező tartalma, gépelésnél tehát minden betűnél. Van még `"click"`,
`"submit"`, `"change"` és még sok másik.

Most már minden gépelésnél újrarajzolódik a lista, csak épp ugyanaz. Szűrjünk. Írd át a
`render` függvényt:

```js
function render() {
  const query = search.value.toLowerCase();

  const filtered = tasks.filter(
    (task) =>
      task.title.toLowerCase().includes(query) || task.description.toLowerCase().includes(query),
  );

  const cards = filtered.map(card);
  list.replaceChildren(...cards);
}
```

Mentsd el, és írd be a keresőbe, hogy `prím`. Egy kártya marad.

- `search.value`: a beírt szöveg. Az `input` elemeknél mindig `value`, nem `textContent`.
- `toLowerCase()` mindkét oldalon: így mindegy, hogy kis vagy nagy betűvel gépelsz.
- `includes()`: igaz, ha a sztringben szerepel a keresett részlet.
- `||`: vagy. Elég, ha a címben **vagy** a leírásban megvan.

## 9. Számláló és üres állapot

Két apróság, amitől használhatóvá válik. Az `index.html`-ben a keresőmező (`<input>`) alá:

```html
<p id="counter" class="mb-4 text-sm text-slate-500"></p>
```

Az `app.js`-ben a `const search` sor alá:

```js
const counter = document.querySelector("#counter");
```

És a `render` függvényben cseréld le az utolsó két sort erre:

```js
counter.textContent = `${filtered.length} feladat`;

if (filtered.length === 0) {
  const message = document.createElement("p");
  message.className = "text-slate-500";
  message.textContent = "Nincs találat.";
  list.replaceChildren(message);
} else {
  const cards = filtered.map(card);
  list.replaceChildren(...cards);
}
```

Mentsd el, és keress rá valamire, ami nincs, például `kvantum`. "0 feladat", és egy
tisztességes üzenet az üres rács helyett.

- Az üzenetet nem sablonból klónozzuk, hanem `createElement`-tel gyártjuk.
- A `className` az elem teljes `class` attribútumát írja felül. Az új elemen még nincs
  semmi, amit elrontana, ezért itt ez a legegyszerűbb.

Ezzel kész a JavaScript rész. A hátralévő két fejezet ugyanezt a kódot fogja
biztonságosabbá tenni.

## 10. TypeScript

### Miért

Keresd meg a `card` függvényben ezt a sort:
`node.querySelector("[data-title]").textContent = task.title;`, és írd át szándékosan a
végét `task.name`-re. Ilyen mező nincs a feladatokon. Mentsd el.

Eltűnt az összes kártya címe. Nincs hibaüzenet, nincs figyelmeztetés, a program vidáman
lefutott. Egy elírt mezőnév, és a kód úgy fut tovább, mintha minden rendben lenne, csak épp
hiányoznak a címek.

Írd vissza, és próbáld ki a másikat: az egyik feladatnál írd át a `difficulty` értékét
`"Hard"`-ra, nagy kezdőbetűvel. Eltűnik az összes kártya, a konzolban pedig ott egy piros
hiba (`TypeError`), ami arról szól, hogy valami `undefined`. A pontos szövege böngészőnként
más, és a Bun az oldalra is kirakja. Ez legalább szól, de csak futás közben, és rossz helyre
mutat: a `card` függvényre, pedig az a jó, az adat a hibás.

Erre való a TypeScript. Ugyanaz a nyelv, plusz annyi, hogy leírhatod, milyen alakú
adatokkal dolgozol. Cserébe a szerkesztőd pirossal aláhúzza a hibát, mielőtt egyszer is
lefuttattad volna.

Javítsd vissza mindkettőt, mielőtt továbbmész.

### Bun

A böngésző nem érti a TypeScriptet. Kell valami, ami lefordítja sima JavaScriptté. Ezt a
Bun csinálja, ugyanaz, amelyik eddig is kiszolgálta az oldalt.

**Nevezd át** az `app.js` fájlt `app.ts`-re, és az `index.html`-ben írd át a `script` sort
is:

```html
<script src="app.ts"></script>
```

A szervert nem kell újraindítani. Amíg az átnevezés és a `script` sor javítása között
vagy, a terminálban egy piros `Could not resolve: "app.js"` hiba jelenik meg: az
`index.html` még a régi fájlt keresi (a végén javasolt `bun install`-lal ne foglalkozz).
Amint elmented a javított sort, a Bun kiírja, hogy újratöltötte az `index.html`-t
(`Reloaded ... index.html`), és az oldal újra működik.

Az oldal ugyanaz, mint eddig, de most a Bun menet közben lefordítja az `app.ts`-t
JavaScriptté, és a böngésző már csak azt kapja meg.

Ahogy átnevezed, a VS Code néhány sort pirossal aláhúz. Egyelőre hagyd őket, a
`tsconfig.json` után megnézzük, mik ezek.

A szervert futtató terminál foglalt. A következő parancsokhoz nyiss mellé egy másodikat a
terminál panel **+** gombjával.

### tsconfig.json

Hozz létre az `app.ts` mellé egy `tsconfig.json` fájlt:

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "lib": ["ES2022", "DOM"],
    "strict": true,
    "noEmit": true
  }
}
```

Ez a TypeScript beállításfájlja, minden valódi projektben van egy.

- `target`: melyik nyelvi verzióra gondoljon. Az ES2022 elég modern ahhoz, hogy minden
  létezzen, amit a leckében használtunk.
- `lib`: milyen beépített dolgok érhetők el. A `DOM` mondja meg, hogy létezik `document` és
  `window`.
- `strict`: minden ellenőrzés bekapcsolva. Több pirosat fogsz látni, és pont ez a lényeg.
- `noEmit`: a TypeScript csak ellenőrizzen, ne fordítson. A fordítás a Bun dolga.

Ellenőrizni így tudsz, a második terminálból:

```
bun x tsc
```

A `bun x` egy eszközt futtat anélkül, hogy telepítenéd a projektbe. Első alkalommal le is
tölti, ezért ír ki pár `Resolving...` sort.

Egy csomó hibát fog kiírni, nagyjából tízet, és a VS Code-ban is több piros lett. Nem
rontottál el semmit: az oldal ugyanúgy működik, a TypeScript csak most néz rá először
szigorúan. Háromféle hiba van köztük:

- `implicitly has an 'any' type`, kétszer: a `card` nem tudja, milyen alakú egy feladat
  (`Parameter 'task'...`), ezért bármit elfogad, és semmit nem tud ellenőrizni. A második,
  hosszabb üzenet ugyanennek a következménye, a `difficulties[task.difficulty]` sorban.
- `'list' is possibly 'null'`, és ugyanez a `template`-re, a `search`-re és a `counter`-re:
  a `querySelector` lehet, hogy nem talál semmit, és akkor `null`-t ad vissza.
- `Property 'value' does not exist on type 'Element'`, és ugyanígy a `content`-ről: túl
  általános típust tud az elemről, nem tudja, hogy az egy `<input>` vagy egy `<template>`.

A következő fejezet sorban eltünteti őket. Minden lépés után futtasd újra a `bun x tsc`-t,
és nézd, hogyan fogy a lista. Ha már nem ír semmit, nincs hiba.

> A `bun index.html` **nem ellenőrzi** a típusokat, csak leszedi őket. Neki mindegy, mit
> írtál, az oldal hibás típusokkal is elindul.
> A hibákat két helyen látod: a VS Code pirossal aláhúzza gépelés közben, a terminálban
> pedig a `bun x tsc` sorolja fel őket.

## 11. Típusok a Feladatbankban

### Az adat

Az `app.ts` legelejére:

```ts
type Difficulty = "easy" | "medium" | "hard";

type Task = {
  title: string;
  topic: string;
  difficulty: Difficulty;
  description: string;
};
```

A `type` egy nevet ad egy alaknak. A `Task` egy objektum négy mezővel. A `Difficulty`
érdekesebb: nem azt mondja, hogy sztring, hanem hogy **pontosan az a három sztring** az
egyik. A `|` itt vagylagos, és **unió típusnak** (union type) hívják.

Most kösd hozzá az adatot. A tömb kezdetét írd át erre:

```ts
const tasks: Task[] = [
```

A `Task[]` annyit tesz: `Task` elemek tömbje.

**Próbáld ki:** írd át az egyik `difficulty` értékét megint `"Hard"`-ra. Azonnal
piros lesz, és a hibaüzenet megmondja, mit fogadna el helyette. Nevezd át az egyik
feladatban a `title` mezőt `name`-re: ugyanúgy szól. Ezt kerestük.

Javítsd vissza. A `bun x tsc` még ugyanazt a tíz hibát írja: leírtuk az adat alakját, de a
függvények még nem tudnak róla.

### A függvények

Írd át a `card` függvény első sorát erre:

```ts
function card(task: Task): DocumentFragment {
```

A paraméter típusa `Task`, a **visszatérési érték** (return value) `DocumentFragment`, mert
a sablon klónja ilyen. Ettől kezdve, ha a függvényen belül `task.`-et írsz, a VS Code
felkínálja a négy mezőt, és bármi mást hibának jelöl.

A `difficulties` objektum is megérdemel egy típust. Az első sora legyen ez:

```ts
const difficulties: Record<Difficulty, { label: string; classes: string[] }> = {
```

A `Record<K, V>` egy objektum, aminek `K` típusú kulcsai és `V` típusú értékei vannak. Itt
az érték maga is objektum, a típusát ugyanúgy írod le, mint a `Task`-ét. Ez két dolgot ad:
ha kifelejtenél egy nehézséget, szól, és a `difficulties[task.difficulty]` garantáltan talál
egy bejegyzést.

A `render` függvény nem ad vissza semmit, ezt a `void` fejezi ki. Az első sora:

```ts
function render(): void {
```

Futtasd a `bun x tsc`-t: nyolc hiba maradt. Eltűnt mindkettő, amelyik `any`-ről szólt: a
`card` most már tudja, hogy `Task`-ot kap, így azt is, hogy a `task.difficulty` a
`difficulties` egyik kulcsa. A maradék mind elemlekérdezés.

### A null problémája

Nézd meg a `render` függvényt: a `list` piros, és a hiba azt mondja, `possibly 'null'`. A
`querySelector` ugyanis lehet, hogy nem talál semmit, ezért a típusa `Element | null`, és
`null`-on nem hívhatsz `replaceChildren`-t.

Két eszköz van rá. Keresd meg a négy elemlekérdezést (nem egymás mellett vannak), és írd
át őket így:

```ts
const template = document.querySelector("#card-template") as HTMLTemplateElement;
const list = document.querySelector("#list")!;
const search = document.querySelector("#search") as HTMLInputElement;
const counter = document.querySelector("#counter")!;
```

- A `!` azt jelenti: "tudom, hogy ez nem `null`". Ez **ígéret**, nem ellenőrzés. Ha tévedsz,
  ugyanazt a futásidejű hibát kapod, mint JavaScriptben. Akkor használd, ha az elem ott van
  a saját HTML-edben, és te tetted oda.
- Az `as` azt jelenti: "kezeld ezt ilyen típusként", trust me bro. A `querySelector` egy általános
  `Element`-et ad vissza, aminek nincs `value` mezője. Egy `<input>`-nak van, ezért kell
  megmondani, hogy ez az. Ugyanez a helyzet a sablonnal: `content` csak
  `HTMLTemplateElement`-en van. Az `as` a `null` lehetőségét is lenyeli, ezért mellé már nem
  kell `!`.

Futtasd a `bun x tsc`-t. A nyolc hiba eltűnt, de jött helyettük öt új, mind a `card`
függvényben. Ez nem visszalépés: eddig a TypeScript azt se tudta, hogy a `template` egy
sablon, így a klónjába bele se tudott nézni. Most, hogy tudja, a klónt is ellenőrzi.

Négy hiba szerint `Node`-on nincs `querySelector`, az ötödik szerint `Node`-ot nem adhatsz
vissza `DocumentFragment`-ként. A `cloneNode` bármilyen csomóponton (node) hívható, ezért a
típusa csak egy általános `Node`. Te tudod, hogy egy sablon tartalmát másolod, ami mindig
töredék, ezért itt is az `as` segít:

```ts
const node = template.content.cloneNode(true) as DocumentFragment;
```

Futtasd újra. Megint öt hiba, de ezek már ismerősek: `possibly 'null'`. A klónon futó négy
`querySelector` ugyanúgy lehet, hogy nem talál semmit (a `badge`-re kettő hiba is jut, mert
két sorban használod). Tegyél `!`-et mind a négy mögé, ugyanazzal az indokkal, mint fent:

```ts
node.querySelector("[data-title]")!.textContent = task.title;
```

```ts
const badge = node.querySelector("[data-difficulty]")!;
```

Futtasd le a `bun x tsc`-t. Most már nem ír semmit, kész vagy.

Amit nem kell típusozni: a `render`-ben a `query` és a `filtered` sorához hozzá sem
nyúltunk, és mégis tudja, hogy az egyik sztring, a másik `Task[]`. A TypeScript a legtöbb
helyen kitalálja magától. Oda írj típust, ahol az **szerződés**: adatszerkezetekre és
függvényaláírásokra. A többit bízd rá.

## Ellenőrizd magad

Ha valamelyiknél elakadsz, nézz vissza a lépésekre.

**Próbáld ki:**

- [ ] Írd be az egyik feladatba, hogy `difficulty: "very hard"`, nézd meg, mit mond a VS
      Code, aztán javítsd
- [ ] Bővítsd a keresőt, hogy a témakörben is keressen, ne csak a címben és a leírásban
- [ ] Rendezd a kártyákat cím szerint ábécébe kirajzolás előtt
      ([`sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)).
      A `sort` az eredeti tömböt rendezi, de a `filtered` amúgy is egy friss tömb, úgyhogy
      itt nem baj. A `toSorted` a mi `tsconfig.json`-unkkal hibát adna.

**Meg tudod mondani?**

- [ ] Mi a különbség a `const` és a `let` között
- [ ] Mit csinál a `map`, mit a `filter`, és mi a különbség
- [ ] Mi a DOM, és miért nem ugyanaz, mint a HTML fájl
- [ ] Miért `textContent`-tel írjuk be a szöveget, és mi baj lenne az `innerHTML`-lel
- [ ] Mit csinál a `<template>` elem
- [ ] Mit jelent a `cloneNode(true)`-ban a `true`
- [ ] Mi a két dolog, amit az `addEventListener` kap
- [ ] Mit csinál a Bun a TypeScripttel, mielőtt a böngésző megkapja
- [ ] Mi a különbség a `bun index.html` és a `bun x tsc` között
- [ ] Mit jelent a `!` és mit az `as` a `querySelector` után

## Önálló feladat

→ [**2-feladat/FELADAT.md**](2-feladat/FELADAT.md)

Kelts életre egy saját listát: adatból rajzolva, kereshetően, TypeScriptben.

## Olvasmányok

- [JavaScript alapok (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types):
  változók, típusok, a nyelv szerkezete
- [Array metódusok (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array):
  a `map` és a `filter` csak kettő a sokból, érdemes végigfutni a listát
- [String metódusok (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String):
  a teljes lista, jóval több van, mint amit a táblázat mutat
- [`<template>` elem (MDN)](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/template):
  a sablon, amit klónozunk
- [addEventListener (MDN)](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener):
  és innen továbbkattintva az összes esemény
- [TypeScript öt percben](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html):
  pont akkora adag, amekkorát ez a lecke használt
- [Everyday Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html):
  a következő adag, ha kedvet kaptál
- [tsconfig referencia](https://www.typescriptlang.org/tsconfig/): mit tud a beállításfájl
- [Bun HTML és fejlesztői szerver](https://bun.sh/docs/bundler/html-static): mit csinál a
  `bun index.html` a háttérben
- [javascript.info](https://javascript.info/): a legjobb ingyenes JavaScript tankönyv, az
  alapoktól a mélyvízig
