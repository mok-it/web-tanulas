# 01. Bevezetés, HTML, CSS, Tailwind

## Mit fogsz csinálni?

Megépíted a **Feladatbank** oldalát: egy fejlécet navigációval, alatta matekfeladatok
kártyáit egy **reszponzív** rácsban, és egy láblécet. Ezt az oldalt a következő leckékben
fogjuk életre kelteni.

Az út odáig három szakasz:

1. [**HTML**](https://developer.mozilla.org/en-US/docs/Web/HTML): mitől oldal egy oldal, mik az elemek, hogyan épül fel egy dokumentum
2. [**CSS**](https://developer.mozilla.org/en-US/docs/Web/CSS): hogyan nézzen ki, saját kézzel írt stílusokkal
3. [**Tailwind**](https://tailwindcss.com/): ugyanaz, csak sokkal gyorsabban

A végén megcsinálod az [önálló feladatot](2-feladat/FELADAT.md).

## Mire lesz szükséged?

- [VS Code](https://code.visualstudio.com/) a [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) és [Tailwind CSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss) bővítményekkel
- Egy böngésző

---

## 1. Az első oldal

Nyisd meg VS Code-ban a `1-start/index.html` fájlt. Ennyi van benne:

```html
<h1>Feladatbank</h1>
Matekfeladatok egy helyen.
<br />
Válassz témakört, és kezdj gondolkodni!
<p>Sakktábla lefedése</p>
<p>Egy 8×8-as sakktábláról levágunk két átellenes sarokmezőt.</p>
```

Kattints jobb gombbal a fájlra a fájllistában, és válaszd a **Open with Live Server**
lehetőséget. Megnyílik a böngésződben.

Ennyire egyszerű. Nem kellett fordítóprogramot telepítened, mert ezt a szerepet most maga a
böngésző tölti be.

Hasonlítsd össze a kódot az eredménnyel. Mit veszel észre?

- A `<h1>` nagy, vastag betűvel jelent meg, ez egy **címsor** (heading).
- A két `<p>` külön sorba került, és van köztük egy kis hely, ezek **bekezdések** (paragraph).
- A `<br />` sortörést csinált, de a két sor közé nem tett akkora helyet, mint a bekezdések
  közé.
- A kacsacsőrös részek maguk **nem látszanak** az oldalon. Ezek nem a tartalom, hanem a
  tartalomról szóló információ.

> Ebben a leckében mentés után **frissítsd a böngészőt** (`F5`), különben nem látod a
> változást. A körforgás végig ez lesz: írsz, mentesz, frissítesz, megnézed.

## 2. HTML dióhéjban

Amit írtunk, az HTML: _HyperText Markup Language_. Egy HTML dokumentum **elemekből** áll:

```html
<típus>szöveg vagy további elemek</típus>
```

- Az elem elejét és végét egy **tag** (címke) jelzi.
- A **nyitó tag** az elem típusa kacsacsőrök között: `<p>`
- A két tag között vannak az elem **gyerekei** (children): további elemek vagy egyszerű szöveg.
- A **záró tag** ugyanaz, csak a típus előtt egy perjellel: `</p>`
- Ha egy elemnek nem lesz gyereke, rövidebben is írható: `<br />`. Egy sortörésbe nyilván
  nem akarunk semmit beletenni.

### Attribútumok

Az elemeknek lehetnek **attribútumaik**, amik extra információt adnak róluk:

```html
<típus attribútum="érték" másik="érték">...</típus>
```

Próbáld ki: másold a fájl végére ezt a két sort.

```html
<a href="https://medvematek.hu">Medve Matek</a>
<img src="https://picsum.photos/id/237/300/200" alt="Fekete labrador kölyökkutya" />
```

- Az `<a>` egy **link** (anchor). A `href` attribútum mondja meg, hova vezet.
- Az `<img>` egy **kép**. A `src` az elérési út, az `alt` pedig a szöveges leírás arra az
  esetre, ha a kép nem tölt be, és ezt olvassa fel a képernyőolvasó a látássérülteknek is.

Nem mindegy, melyik elemhez milyen attribútumot adsz: mindegyiknek megvan a maga készlete.

> **Komment**, mint minden nyelvben: `<!-- ezt a böngésző figyelmen kívül hagyja -->`.
> Gyakran arra használjuk, hogy valamit ideiglenesen kivegyünk a kódból.

## 3. Fej, tor, potroh

Eddig egy töredéket írtunk. Egy rendes HTML dokumentumnak van egy kötelező váza:

- `<!DOCTYPE html>`: jelzés a böngészőnek, hogy ez egy HTML dokumentum
- `<html>`: a gyökérelem, ebben van minden más
- `<head>`: ide kerül minden, ami **nem látszik** az oldalon, de tudni kell róla
- `<body>`: ide kerül minden, ami **látszik**

Cseréld le a `1-start/index.html` **teljes** tartalmát erre:

```html
<!DOCTYPE html>
<html lang="hu">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Feladatbank</title>
  </head>
  <body>
    <h1>Feladatbank</h1>
    Matekfeladatok egy helyen. <br />
    Válassz témakört, és kezdj gondolkodni!
    <p>Sakktábla lefedése</p>
    <p>Egy 8×8-as sakktábláról levágunk két átellenes sarokmezőt.</p>
    <a href="https://medvematek.hu">Medve Matekverseny</a>
    <img src="https://picsum.photos/id/237/300/200" alt="Fekete labrador kölyökkutya" />
  </body>
</html>
```

Az oldal maga alig változott, viszont nézd meg a böngészőlap fülét: most már
`Feladatbank` a neve, a `<title>` miatt.

Amit a `<head>`-be tettünk:

| Elem                         | Mire jó                                                                 |
| ---------------------------- | ----------------------------------------------------------------------- |
| `<meta charset="UTF-8">`     | Karakterkódolás. **Enélkül az ékezetes betűk krikszkrakszok lehetnek.** |
| `<meta name="viewport" ...>` | Mobilon ettől lesz értelmes az oldal mérete                             |
| `<title>`                    | A böngészőlap neve                                                      |

Az `<html lang="hu">` pedig megmondja, hogy magyar nyelvű az oldal. Ezt a keresők és a
képernyőolvasók használják.

## 4. Szemantikus elemek és az első feladatkártya

A `<div>` egy általános "doboz" elem, amivel bármit körbe lehet keríteni. Meg lehetne
csinálni belőle az egész oldalt, csak épp senki nem tudná, melyik doboz mi.

Ezért van a HTML-ben egy csomó elem, ami **ugyanúgy néz ki, mint egy `div`, de jelent is
valamit**:

| Elem        | Mit jelent                                                         |
| ----------- | ------------------------------------------------------------------ |
| `<header>`  | Az oldal (vagy egy szakasz) fejléce                                |
| `<nav>`     | Navigáció, linkek gyűjteménye                                      |
| `<main>`    | Az oldal fő tartalma. Egy oldalon egy darab van belőle             |
| `<section>` | Egy önálló szakasz a tartalomban                                   |
| `<article>` | Egy önmagában is megálló tartalomegység, például egy feladatkártya |
| `<footer>`  | Lábléc                                                             |

Ez nem szőrszálhasogatás: ebből tudja a képernyőolvasó, hogy átugorhatja a navigációt, és
ebből tudja a Google, hogy mi az oldal lényege.

Írjuk meg az első feladatkártyát. Cseréld le a `<body>` **teljes** tartalmát erre:

```html
<header>
  <h1>Feladatbank</h1>
  <nav>
    <a href="#">Feladatok</a>
    <a href="#">Témakörök</a>
    <a href="#">Rólunk</a>
  </nav>
</header>

<main>
  <h2>Feladatok</h2>

  <article>
    <h3>Sakktábla lefedése</h3>
    <p><span>Kombinatorika</span> <span>könnyű</span></p>
    <p>
      Egy 8×8-as sakktábláról levágunk két átellenes sarokmezőt. Lefedhető-e a maradék 62
      mező 31 darab 1×2-es dominóval?
    </p>
  </article>
</main>

<footer>
  <p>Mök IT · Web tanulás</p>
</footer>
```

Csúnya, de **szerkezete van**.

Két új dolog:

- A `href="#"` egy link, ami sehova nem visz. Ez a szokásos helykitöltő, amíg nincs meg az
  igazi cél.
- A `<span>` a `<div>` soron belüli megfelelője: egy jelentés nélküli doboz, amivel a
  szöveg egy darabját tudjuk megfogni, hogy később megstílusozzuk.

> Nyisd meg a fejlesztői eszközöket (`F12`), és menj az `Elements` fülre. Ott a te HTML-edet
> látod fa formában, kinyitható ágakkal. Ha ráviszed az egeret egy elemre, a böngésző
> kiemeli az oldalon. Ez lesz a legfontosabb eszközöd, amikor valami nem úgy néz ki, ahogy
> szeretnéd.

---

## 5. CSS: hogyan nézzen ki

A HTML megmondja, **mi** van az oldalon. A CSS megmondja, **hogy nézzen ki**. A neve
_Cascading Style Sheets_.

Hozz létre a `1-start/` mappában egy `styles.css` nevű fájlt, és tedd bele ezt:

```css
body {
  font-family: system-ui, sans-serif;
  background-color: #f1f5f9;
  color: #0f172a;
  margin: 0;
  padding: 2rem;
}
```

Ettől még nem történik semmi: a HTML-nek nem szóltunk a fájlról. Tedd ezt a `<head>`-be, a
`<title>` alá:

```html
<link rel="stylesheet" href="styles.css" />
```

A háttér halványkék lett, a betűtípus megváltozott.

### Amit írtunk

```css
selector {
  tulajdonság: érték;
}
```

- A **selector** megmondja, **mire** vonatkozik a **szabály** (rule). A `body` az összes `<body>`
  elemre, amiből egy van.
- Utána kapcsos zárójelben jönnek a **tulajdonság: érték** párok, pontosvesszővel elválasztva.

### Selectorok

Háromféle selectorral fogsz a leggyakrabban találkozni:

```css
p { }          /* minden <p> elem */
.kartya { }    /* minden elem, aminek class="kartya" az attribútuma */
#fejlec { }    /* az az egy elem, aminek id="fejlec" */
```

A `class` a fontos: ugyanazt az osztályt **tetszőlegesen sok** elemre ráteheted, és egy
elemnek **több osztálya is lehet**, szóközzel elválasztva. Az `id`-nak egyedinek kell
lennie az oldalon, ezért ritkábban használjuk stílusozásra.

### Selectorok kombinálása

Ezeket össze lehet fűzni, és ilyenkor **a szóköz is jelent valamit**:

```css
.cimke.nehezseg { }   /* egy elem, aminek MINDKÉT osztálya megvan */
.kartya .cimke { }    /* .cimke, ami egy .kartya elemen BELÜL van, bármilyen mélyen */
.kartya > .cimke { }  /* .cimke, ami közvetlenül a .kartya gyereke */
p.kartya-leiras { }   /* p elem, aminek kartya-leiras az osztálya */
h1, h2, h3 { }        /* mindhárom, a vessző vagylagos */
```

Az első kettő közti különbség a leggyakoribb kezdő hiba. A `.cimke.nehezseg` **egyetlen**
elemet ír le, aminek két osztálya van. A `.cimke .nehezseg` **két** elemet, ahol az egyik a
másikon belül van. Egy szóköz a különbség.

Az összefűzésnek nincs felső korlátja: a `header nav > a` azt jelenti, hogy egy `a` elem,
ami közvetlenül egy `nav` gyereke, ami pedig valahol egy `header`-en belül van.

> A teljes lista, az összes kombinátorral és a példákkal:
> [Selectors and combinators (MDN)](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_selectors/Selectors_and_combinators).
> Van még néhány, amire ritkábban van szükség, például a `+` a közvetlenül utána következő
> testvérre, vagy a `[href]` az adott attribútummal rendelkező elemekre.

### Adjunk osztályokat

Írd át a `<article>` elemet így (a belseje marad):

```html
<article class="kartya">
  <h3 class="kartya-cim">Sakktábla lefedése</h3>
  <p><span class="cimke">Kombinatorika</span> <span class="cimke nehezseg">könnyű</span></p>
  <p class="kartya-leiras">
    Egy 8×8-as sakktábláról levágunk két átellenes sarokmezőt. Lefedhető-e a maradék 62
    mező 31 darab 1×2-es dominóval?
  </p>
</article>
```

Figyeld meg a `class="cimke nehezseg"` részt: ez az elem **két** osztályba is tartozik.
Mindkettő szabályai érvényesek rá.

Most a `styles.css` végére:

```css
.kartya {
  background-color: white;
  border: 1px solid #cbd5e1;
  border-radius: 8px;
  padding: 16px;
  max-width: 320px;
}

.kartya-cim {
  margin: 0 0 8px 0;
  font-size: 18px;
}

.kartya-leiras {
  color: #475569;
  font-size: 14px;
  line-height: 1.5;
}

.cimke {
  display: inline-block;
  background-color: #e2e8f0;
  color: #334155;
  border-radius: 999px;
  padding: 2px 10px;
  font-size: 12px;
}

.nehezseg {
  background-color: #d1fae5;
  color: #065f46;
}
```

Most már kártyának néz ki.

> A `nehezseg` osztály felülírja a `cimke` háttérszínét, mert **később** szerepel a
> fájlban. Ez a "cascading" a CSS nevében: ha több szabály is vonatkozik egy elemre,
> szabályok döntik el, melyik nyer. A leggyakoribb eset ez: az utolsó nyer.

### A doboz-modell

Minden HTML elem egy téglalap, aminek négy rétege van kívülről befelé. Ez a **doboz-modell**:

```
┌─────────────────────── margin ────────────────────────┐
│  ┌───────────────────── border ────────────────────┐  │
│  │  ┌─────────────────  padding  ───────────────┐  │  │
│  │  │                                           │  │  │
│  │  │              tartalom                     │  │  │
│  │  │                                           │  │  │
│  │  └───────────────────────────────────────────┘  │  │
│  └─────────────────────────────────────────────────┘  │
└───────────────────────────────────────────────────────┘
```

- **padding**: belső térköz, a tartalom és a keret között. A háttérszín ide is kiterjed.
- **border**: a keret maga.
- **margin**: külső térköz, a szomszédos elemekig. Ez mindig átlátszó.

Ezt a négy réteget látni is tudod: `F12` → `Elements` → válassz ki egy elemet → a jobb
oldali panelen görgess le a `Computed` fülig. Ott van a doboz-modell rajz a konkrét
értékekkel. Ha valami "nem oda kerül, ahova akarom", jó eséllyel itt fogod megtalálni, miért.

## 6. Flexbox elrendezés

Másold le a kártyát, hogy három legyen belőle (`Ctrl+C`, `Ctrl+V` az egész `<article>`
blokkra), és írd át a második és harmadik címét valamire.

Egymás alatt vannak. Tegyük őket egymás mellé.

Kerítsd körbe a kártyákat egy `div`-vel:

```html
<div class="sor">
  <article class="kartya">...</article>
  <article class="kartya">...</article>
  <article class="kartya">...</article>
</div>
```

És a CSS-be:

```css
.sor {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
}
```

Egymás mellé kerültek.

A [`display: flex`](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_flexible_box_layout) azt mondja: **ennek az elemnek a gyerekeit rendezd sorba**. Nem magát az
elemet változtatja meg, hanem azt, hogyan viselkednek benne a gyerekei.

| Tulajdonság       | Mit csinál                                                     |
| ----------------- | -------------------------------------------------------------- |
| `flex-direction`  | A fő tengely iránya: `row` egymás mellé, `column` egymás alá   |
| `gap`             | Térköz a gyerekek között                                       |
| `justify-content` | Igazítás a fő tengely mentén (`center`, `space-between`, ...)  |
| `align-items`     | Igazítás a fő tengelyre merőlegesen (`center`, `stretch`, ...) |
| `flex-wrap`       | `wrap` értékkel új sorba törnek a gyerekek, ha nem férnek ki   |

> Ez csak a leggyakrabban használt öt. A flexbox teljes leírása egy oldalon, ábrákkal
> minden tulajdonsághoz:
> [A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/).

Rendezzük el a fejlécet is. A CSS végére:

```css
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 24px;
}

nav {
  display: flex;
  gap: 16px;
}
```

A cím balra, a navigáció jobbra került, függőlegesen egymáshoz igazítva.

> A `justify-content: space-between` a leggyakrabban használt trükk a weben: az első elem
> balra, az utolsó jobbra, a maradék hely egyenletesen elosztva közöttük.

Most nézd meg, mit írtál eddig a `styles.css`-be. Hét szabály, egyetlen kártyához és egy
fejléchez. És még nincs hover, nincs árnyék, nincs mobilnézet.

Itt jön be a Tailwind.

---

## 7. Tailwind: stílus a HTML-ben

A Tailwind egy CSS keretrendszer, ami egy szokatlan ötletre épül: **ne írj CSS-t, hanem
rakd össze a stílust apró, egy dolgot csináló osztályokból**, közvetlenül a HTML-ben.

Ezek az osztályok ilyenek:

| Tailwind osztály | Amit helyettesít          |
| ---------------- | ------------------------- |
| `p-4`            | `padding: 16px`           |
| `bg-white`       | `background-color: white` |
| `text-sm`        | `font-size: 14px`         |
| `flex`           | `display: flex`           |
| `gap-4`          | `gap: 16px`               |
| `rounded-lg`     | `border-radius: 8px`      |

Egy Tailwind-es kártya nyitótagja így néz ki:

```html
<article class="rounded-lg border border-slate-200 bg-white p-4">
```

Első ránézésre ez borzalom: minek a HTML-be stílust írni, amikor épp az a CSS lényege, hogy
külön van? A gyakorlatban viszont ez működik jól, és ezért:

- **Nem kell nevet kitalálnod.** A `.kartya-cim` osztálynévről órákat lehet vitatkozni.
- **Nem kell két fájl között ugrálnod.** Amit látsz, azt írod.
- **Nem nő a végtelenségig.** Ahogy a projekt nő, a saját CSS fájlod egyre nagyobb lesz, és
  soha nem mered kitörölni belőle a szabályokat, mert nem tudod, ki használja még. A
  Tailwind osztályok ott élnek és halnak, ahol használod őket.
- **Konzisztens.** A `p-4` mindig 16px. Nem lesz az oldaladon 14, 15 és 16 pixeles térköz.

### Húzzuk be

Élesben a Tailwindet be szoktuk építeni a projektbe (ezt majd az 5. leckében látod), de van  
egy változat, ami egyetlen `script` taggel működik. Tedd ezt a `head`-be:

```html
<script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
```

> Ez a `script` a böngészőben fordítja le a Tailwindet menet közben. Tanuláshoz és
> kísérletezéshez tökéletes, **éles oldalra nem való**, ott lassabb, mint kellene. Az 5. leckében látni fogod a rendes megoldást.

És **töröld ki** a `styles.css`-re mutató `link` sort, innentől nem lesz rá szükség. A
`styles.css` fájlt hagyd meg, hogy vissza tudj nézni rá.

Ugyanígy töröld ki a **két másolt kártyát** is, elég egy. Azokat csak azért csináltuk, hogy
legyen mit egymás mellé rendezni a flexboxszal.

Az oldal most csupasz. Ennek két oka van: a saját CSS-ünket kivettük, a Tailwind pedig az
első dolgok között minden elem alapértelmezett stílusát nullázza, hogy tiszta lapról
indulj.

> Innentől néhány lépésen át az oldalad félkésznek fog kinézni: előbb a kártyát írjuk át,  
> aztán a fejlécet, a törzset és a láblécet.

### Írjuk át a kártyát

Cseréld le az első `article` elemet erre:

```html
<article class="rounded-lg border border-slate-200 bg-white p-5 shadow-sm">
  <h3 class="mb-2 text-lg font-semibold">Sakktábla lefedése</h3>
  <div class="mb-3 flex flex-wrap gap-2">
    <span class="rounded-full bg-slate-100 px-2.5 py-0.5 text-xs text-slate-700">
      Kombinatorika
    </span>
    <span class="rounded-full bg-emerald-100 px-2.5 py-0.5 text-xs text-emerald-800">
      könnyű
    </span>
  </div>
  <p class="text-sm leading-relaxed text-slate-600">
    Egy 8×8-as sakktábláról levágunk két átellenes sarokmezőt. Lefedhető-e a maradék 62 mező
    31 darab 1×2-es dominóval?
  </p>
</article>
```

Ugyanaz a kártya, CSS fájl nélkül.

Vidd rá az egeret VS Code-ban egy osztálynévre, például a `text-slate-600`-ra. A Tailwind
CSS IntelliSense megmutatja, milyen CSS-t jelent. Ha elakadsz, ez a leggyorsabb módja
kideríteni, mit csinál valami.

### A számrendszer

A legtöbb Tailwind osztály végén egy szám van. Kétféle skála létezik:

- **Méretek** (`p-4`, `gap-2`, `mb-3`): a szám négyszerese pixelben. Tehát `p-4` = 16px,
  `gap-2` = 8px.
- **Színek** (`slate-100`, `slate-600`, `emerald-800`): 50-től 950-ig, a világostól a
  sötétig. A `slate-100` majdnem fehér, a `slate-900` majdnem fekete.

Ez a két skála a Tailwind lényegi haszna: kötött választékból dolgozol, ezért nem tudsz
egymáshoz nem illő értékeket összerakni.

## 8. A fejléc és a lábléc

A kártya kész, de körülötte még minden csupasz. Haladjunk kívülről befelé.

Először a `body`. Adj neki osztályokat, hogy legyen háttérszín és alapértelmezett
szövegszín:

```html
<body class="bg-slate-100 text-slate-900">
```

Most a fejléc. Cseréld le a teljes `header` blokkot erre:

```html
<header class="border-b border-slate-200 bg-white">
  <div class="mx-auto flex max-w-5xl items-center justify-between px-6 py-4">
    <h1 class="text-xl font-bold">Feladatbank</h1>
    <nav class="flex gap-5 text-sm text-slate-600">
      <a href="#" class="hover:text-slate-900">Feladatok</a>
      <a href="#" class="hover:text-slate-900">Témakörök</a>
      <a href="#" class="hover:text-slate-900">Rólunk</a>
    </nav>
  </div>
</header>
```

A fejléc fehér sávja végigmegy a képernyőn, a tartalma viszont középen van, és
nem ér ki a széléig.

Két dolog, amit érdemes megjegyezni:

- A `mx-auto max-w-5xl px-6` hármas a web egyik legtöbbet használt mintája: legyen
  legfeljebb ilyen széles, azon belül középen, és legyen oldalt egy kis levegő, hogy
  mobilon ne érjen a képernyő széléhez. Ezért van a `header` belsejében egy külön `div`:
  a fehér háttér és az alsó keret a teljes szélességet fogja, a tartalom viszont nem.
- A `hover:text-slate-900` a linkeken azt jelenti, hogy amikor az egér fölöttük van,
  sötétebbek lesznek. Vidd rá az egeret, és nézd meg.

Most a lábléc. Cseréld le a teljes `footer` blokkot erre:

```html
<footer class="border-t border-slate-200 py-6 text-center text-sm text-slate-500">
  Mök IT · Web tanulás
</footer>
```

A `p` elem kikerült belőle, mert a szövegre vonatkozó osztályokat ráraktuk magára a
`footer`-re.

## 9. A rács

Következik a `main`. Adj neki ugyanolyan középre igazítást, mint a fejléc belsejének, és
állítsd be a címsort is:

```html
<main class="mx-auto max-w-5xl px-6 py-8">
  <h2 class="mb-6 text-2xl font-bold">Feladatok</h2>
```

Most a kártyák konténere. A `sor` osztály a saját CSS fájlunkból jött, ami már nincs
belinkelve, tehát jelenleg nem csinál semmit. Cseréld le erre:

```html
<div class="grid grid-cols-3 gap-4">
```

Egy kártya van egy háromoszlopos rácsban, ezért a szélesség egyharmadát
foglalja el.

A flexbox sorba rendez, a grid rácsba. A `grid` osztály ugyanúgy a szülőre kerül, mint a
`flex`, és ugyanúgy a gyerekek elrendezését határozza meg.

A leggyakrabban használt osztályok:

| Osztály       | Mit csinál                                                       |
| ------------- | ---------------------------------------------------------------- |
| `grid`        | `display: grid`, ettől lesz rács az elem                         |
| `grid-cols-3` | Három egyenlő szélességű oszlop. A szám 1-től 12-ig mehet        |
| `gap-4`       | Térköz a cellák között. Külön is állítható: `gap-x-4`, `gap-y-2` |
| `col-span-2`  | Ez az **egyik gyerek** két oszlopot foglaljon el a három helyett |
| `grid-rows-2` | Sorok száma, ha nem akarod a böngészőre bízni                    |
| `row-span-2`  | Ez az egyik gyerek két sor magas legyen                          |
| `items-start` | A cellákon belül felülre igazítsa a tartalmat `stretch` helyett  |

Az utolsó négyre ebben a leckében nem lesz szükséged, de jó tudni, hogy léteznek: ezekkel
lehet olyan rácsot építeni, ahol az egyik elem nagyobb helyet kap, mint a többi.

> A grid teljes leírása, a flexboxos párja ugyanarról az oldalról:
> [A Complete Guide to CSS Grid](https://css-tricks.com/snippets/css/complete-guide-grid/).
> Ez a kettő együtt lefedi a weben az elrendezések nagyjából egészét.

## 10. Állapotok: pszeudo osztályok

Egészítsd ki a meglévő kártya osztálylistáját két osztállyal a végén:

```html
<article class="rounded-lg border border-slate-200 bg-white p-5 shadow-sm transition hover:shadow-md">
```

Vidd rá az egeret a kártyára. Megemelkedik.

Aminek most örülsz, annak CSS-ben **pszeudo osztály** (pseudo-class) a neve. Egy pszeudo
osztály bármelyik selector mögé odaírható, és a szabály érvényességét az elem egy konkrét állapotára szűkíti.
Kézzel írt CSS-ben így nézne ki:

```css
.kartya {
  box-shadow: 0 1px 2px rgb(0 0 0 / 0.05);
}

.kartya:hover {
  box-shadow: 0 4px 6px rgb(0 0 0 / 0.1);
}
```

A Tailwind ugyanezt csinálja, csak előtagként. A `hover:shadow-md`-ből nagyjából ez lesz:

```css
@media (hover: hover) {
  .hover\:shadow-md:hover {
    box-shadow:
      0 4px 6px -1px rgb(0 0 0 / 0.1),
      0 2px 4px -2px rgb(0 0 0 / 0.1);
  }
}
```

Ugyanaz a minta, mint a töréspontoknál: az osztálynévben benne van a kettőspont, a selector
végén pedig ott a valódi `:hover`.

> Figyeld meg a `@media (hover: hover)` burkolót. A szabály csak ott érvényes, ahol tényleg
> van egérmutató. Érintőképernyőn nincs "ráhúzás", ezért a Tailwind eleve kihagyja.
> Kézzel írt CSS-ben ez gyakori hibaforrás: mobilon a `:hover` koppintás után beragad, és
> csak akkor tűnik el, ha máshova koppintasz.

A `transition` azért kell, hogy az árnyék ne ugorva váltson, hanem átúszzon. Vedd ki egy
pillanatra, és vidd rá megint az egeret. Érezhető a különbség.

### A gyakoriak

| CSS                | Tailwind    | Mikor érvényes                           |
| ------------------ | ----------- | ---------------------------------------- |
| `:hover`           | `hover:`    | Az egér az elem fölött van               |
| `:active`          | `active:`   | Épp le van nyomva                        |
| `:focus`           | `focus:`    | Fókuszban van, kattintás vagy `Tab` után |
| `:disabled`        | `disabled:` | Letiltott űrlapelem                      |
| `:first-child`     | `first:`    | A testvérei közül az első                |
| `:last-child`      | `last:`     | A testvérei közül az utolsó              |
| `:nth-child(even)` | `even:`     | Páros sorszámú testvér                   |

Az első négy **interaktív**: a felhasználótól függ. Az utolsó három **struktúra szerinti**:
attól függ, hányadik az elem a testvérei között. Ez utóbbiakkal lehet például minden
második táblázatsort csíkozni anélkül, hogy egyenként osztályt adnál nekik.

### Próbáld ki

Add hozzá mindhárom navigációs linkhez az `active:text-slate-400` osztályt a meglévő
`hover:text-slate-900` mellé:

```html
<a href="#" class="hover:text-slate-900 active:text-slate-400">Feladatok</a>
```

Nyomj rá egy linkre, és **ne engedd fel** az egérgombot. Amíg nyomva tartod,
halványabb.

Most nyomogasd a `Tab` billentyűt. Ahogy végigugrálsz a linkeken, mindegyik körül megjelenik
egy keret: ez a `:focus` állapot, amit a böngésző alapból ad. Ez teszi lehetővé, hogy
egér nélkül, billentyűzetről is használható legyen az oldal. **Soha ne tüntesd el anélkül,
hogy mást raknál a helyére.**

### Pszeudo elemek

Van egy másik fajta is, ami hasonlóan néz ki, de mást csinál. A **pszeudo elem**
(pseudo-element) nem állapotra szűkít, hanem létrehoz egy virtuális gyerekelemet, ami nincs benne a HTML-ben.
Megkülönböztetésül **dupla** kettősponttal írjuk:

```css
.cimke::before {
  content: "#";
}
```

Tailwindben ugyanez `before:` előtaggal, és a tartalom is osztályként megy. Próbáld ki a
kártyád témakör-címkéjén: tedd a `before:content-['#']` osztályt a többi mellé.

```html
<span class="rounded-full bg-slate-100 px-2.5 py-0.5 text-xs text-slate-700 before:content-['#']">
  Kombinatorika
</span>
```

A címkéből `#Kombinatorika` lett, pedig a `#` nincs benne a HTML-ben. Nézd meg az
`Elements` fülön: külön `::before` csomópontként jelenik meg, nem a szöveg részeként.

Ez most csak kísérlet, a lecke többi része nem számít rá. Hagyd meg, ha tetszik, vagy vedd
ki nyugodtan.

A tartalmat mindig meg kell adni, különben a pszeudo elem meg sem jelenik. A `::before` és
`::after` klasszikus felhasználása a kötelező űrlapmezők megjelölése piros csillaggal,
anélkül hogy minden címkébe kézzel beleírnád.

> Egy pszeudo elem csak a selector **legvégén** állhat. A `div::after:hover` érvénytelen.
> Fordítva viszont működik: `div:hover::after`.

## 11. A többi kártya

Másold be az öt új kártyát a meglévő `article` **után**, még a rácsot tartó
`div`-en belülre:

```html
<article class="rounded-lg border border-slate-200 bg-white p-5 shadow-sm transition hover:shadow-md">
  <h3 class="mb-2 text-lg font-semibold">Hamis érme</h3>
  <div class="mb-3 flex flex-wrap gap-2">
    <span class="rounded-full bg-slate-100 px-2.5 py-0.5 text-xs text-slate-700">Logika</span>
    <span class="rounded-full bg-amber-100 px-2.5 py-0.5 text-xs text-amber-800">közepes</span>
  </div>
  <p class="text-sm leading-relaxed text-slate-600">
    Adott 12 egyforma érme, köztük egy hamis, ami a többinél könnyebb vagy nehezebb.
    Találd meg három mérlegeléssel egy kétkarú mérlegen!
  </p>
</article>

<article class="rounded-lg border border-slate-200 bg-white p-5 shadow-sm transition hover:shadow-md">
  <h3 class="mb-2 text-lg font-semibold">Végtelen sok prím</h3>
  <div class="mb-3 flex flex-wrap gap-2">
    <span class="rounded-full bg-slate-100 px-2.5 py-0.5 text-xs text-slate-700">Számelmélet</span>
    <span class="rounded-full bg-amber-100 px-2.5 py-0.5 text-xs text-amber-800">közepes</span>
  </div>
  <p class="text-sm leading-relaxed text-slate-600">
    Bizonyítsd be, hogy végtelen sok prímszám van! A bizonyítás Eukleidésztől származik,
    és elfér néhány sorban.
  </p>
</article>

<article class="rounded-lg border border-slate-200 bg-white p-5 shadow-sm transition hover:shadow-md">
  <h3 class="mb-2 text-lg font-semibold">Königsbergi hidak</h3>
  <div class="mb-3 flex flex-wrap gap-2">
    <span class="rounded-full bg-slate-100 px-2.5 py-0.5 text-xs text-slate-700">Gráfelmélet</span>
    <span class="rounded-full bg-emerald-100 px-2.5 py-0.5 text-xs text-emerald-800">könnyű</span>
  </div>
  <p class="text-sm leading-relaxed text-slate-600">
    Königsberg városát hét híd köti össze. Bejárható-e úgy a város, hogy minden hídon
    pontosan egyszer megyünk át?
  </p>
</article>

<article class="rounded-lg border border-slate-200 bg-white p-5 shadow-sm transition hover:shadow-md">
  <h3 class="mb-2 text-lg font-semibold">Skatulyaelv a bulin</h3>
  <div class="mb-3 flex flex-wrap gap-2">
    <span class="rounded-full bg-slate-100 px-2.5 py-0.5 text-xs text-slate-700">Kombinatorika</span>
    <span class="rounded-full bg-amber-100 px-2.5 py-0.5 text-xs text-amber-800">közepes</span>
  </div>
  <p class="text-sm leading-relaxed text-slate-600">
    Egy hatfős társaságban bárki bárkit vagy ismer, vagy nem. Bizonyítsd be, hogy mindig
    van három ember, akik páronként ismerik egymást, vagy három, akik páronként nem!
  </p>
</article>

<article class="rounded-lg border border-slate-200 bg-white p-5 shadow-sm transition hover:shadow-md">
  <h3 class="mb-2 text-lg font-semibold">Hilbert szállodája</h3>
  <div class="mb-3 flex flex-wrap gap-2">
    <span class="rounded-full bg-slate-100 px-2.5 py-0.5 text-xs text-slate-700">Halmazelmélet</span>
    <span class="rounded-full bg-rose-100 px-2.5 py-0.5 text-xs text-rose-800">nehéz</span>
  </div>
  <p class="text-sm leading-relaxed text-slate-600">
    A szállodában végtelen sok szoba van, és mind foglalt. Érkezik egy új vendég. Hogyan
    szállásolod el? És ha végtelen sokan érkeznek egyszerre?
  </p>
</article>
```

Hat kártya, három oszlopban.

Figyeld meg a nehézség-címkék színét: `emerald` a könnyűnek, `amber` a közepesnek, `rose`
a nehéznek. Ez a fajta apró vizuális kód sokat segít abban, hogy egy listát át lehessen
látni egy pillantással.

## 12. Reszponzivitás

Húzd össze a böngészőablakot keskenyre. A három oszlop megmarad, a kártyák összenyomódnak,
és a szöveg olvashatatlanul keskeny hasábokba tördelődik. Telefonon ez használhatatlan
lenne.

A megoldás az, hogy megmondjuk: három oszlop csak nagy kijelzőn kell. Cseréld le a rácsot
tartó `div` osztálylistáját erre:

```html
<div class="grid gap-4 sm:grid-cols-2 lg:grid-cols-3">
```

Húzd össze újra az ablakot. Most átrendeződik.

A `sm:` és `lg:` előtagok azt jelentik: "ettől a képernyőszélességtől felfelé". A
`grid gap-4 sm:grid-cols-2 lg:grid-cols-3` tehát:

- alapból, mobilon: egy oszlop
- `sm:`, azaz 640px-től: két oszlop
- `lg:`, azaz 1024px-től: három oszlop

Figyeld meg, hogy a `grid-cols-3` eltűnt a listából, és a helyére `lg:grid-cols-3` került.
Mivel előtag nélkül egyáltalán nem adtunk meg oszlopszámot, a legkisebb kijelzőn a rács
egyoszlopos marad.

### Mi lesz ebből CSS-ben?

A Tailwind nagyjából ezt a CSS-t állítja elő a három osztályunkból:

```css
.grid {
  display: grid;
}

@media (width >= 40rem) {
  .sm\:grid-cols-2 {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}

@media (width >= 64rem) {
  .lg\:grid-cols-3 {
    grid-template-columns: repeat(3, minmax(0, 1fr));
  }
}
```

Két dolog fontos ebben:

- Az `sm:grid-cols-2` egy **sima osztálynév**, amiben véletlenül van egy kettőspont. A CSS  
  a kettőspontot máshogy használja, ezért került  elé egy visszaperjel: `.sm\:grid-cols-2`.
  Nem nyelvi elem tehát, csak egy név.
- Az előtag egy `@media` blokkba csomagolja a szabályt. Az ilyen feltételes CSS neve
  **media query**, és ez a reszponzív web alapja, Tailwind nélkül is. A Tailwind csak
  kényelmesebbé teszi: nem kell külön helyen megírnod, és nem kell nevet adnod neki.

Innen látszik, miért **mobile-first** a Tailwind: a `@media (width >= 40rem)` csak
**felfelé** szab feltételt. Az előtag nélküli osztály ezért mindig érvényes, a töréspontos
(breakpoint) pedig felülírja nagyobb kijelzőn. Ezért nincs a "mobil" méretnek saját előtagja: az az
alapeset.

A töréspontok:

| Előtag | Ettől a szélességtől |
| ------ | -------------------- |
| `sm:`  | 40rem (640px)        |
| `md:`  | 48rem (768px)        |
| `lg:`  | 64rem (1024px)       |
| `xl:`  | 80rem (1280px)       |
| `2xl:` | 96rem (1536px)       |

> Ugyanez a logika nem csak az oszlopszámra működik, hanem bármelyik osztályra.
> Írhatsz `text-sm md:text-base`-t, `p-4 lg:p-8`-at, vagy `hidden md:flex`-et, ha valamit
> csak nagyobb kijelzőn akarsz megmutatni.

---

## Ellenőrizd magad

Ha valamelyiknél elakadsz, nézz vissza a lépésekre.

**Próbáld ki:**

- [ ] Állítsd át a rácsot úgy, hogy nagyon széles kijelzőn négy oszlop legyen
- [ ] Írd át az egyik feladat nehézségét `nehéz`-re úgy, hogy a címke színe is stimmeljen
- [ ] Tedd a navigációt a cím mellé balra ahelyett, hogy a jobb szélen lenne
- [ ] Vedd ki a `max-w-5xl` osztályt a `main`-ből, nézd meg mi változik, aztán tedd vissza

**Meg tudod mondani?**

- [ ] Mi a különbség a `head` és a `body` között
- [ ] Mi a különbség egy `div` és egy `article` között
- [ ] Mit csinál a `class` attribútum, és lehet-e egy elemnek több
- [ ] A doboz-modell négy rétegét kívülről befelé
- [ ] Hol találod a böngészőben a doboz-modell rajzát egy kiválasztott elemhez
- [ ] Mit csinál a `display: flex`
- [ ] Mit jelent a `p-4` és mit a `bg-slate-100`
- [ ] Mit jelent az `md:` előtag, és melyik irányba hat
- [ ] Mit csinál a `hover:shadow-md` osztály
- [ ] Mi a különbség a `:hover` és a `::after` között

## Önálló feladat

→ [**2-feladat/FELADAT.md**](2-feladat/FELADAT.md)

Csinálj egy saját oldalt szabadon választott témáról, ugyanezekkel az eszközökkel.

## Olvasmányok

- [HTML elemek listája (MDN)](https://developer.mozilla.org/en-US/docs/Web/HTML/Element):
  ha kíváncsi vagy, mi minden létezik még
- [Tailwind dokumentáció](https://tailwindcss.com/docs): a bal felső kereső a barátod
- [Pszeudo osztályok (MDN)](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)
  és [pszeudo elemek (MDN)](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements):
  a teljes lista, sokkal több van, mint amit a lecke mutat
- [Hover, focus és a többi állapot](https://tailwindcss.com/docs/hover-focus-and-other-states):
  az összes Tailwind előtag egy helyen
- [A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/):
  a legjobb flex referencia, minden tulajdonság egy oldalon, ábrákkal
- [A Complete Guide to CSS Grid](https://css-tricks.com/snippets/css/complete-guide-grid/):
  ugyanaz rácsokra
- [Flexbox Froggy](https://flexboxfroggy.com/#hu): játék, amiben 24 pályán megtanulod a flexboxot.
- [Grid Garden](https://cssgridgarden.com/#hu): ugyanez rácsokra
