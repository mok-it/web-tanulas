# Web tanulás

Interaktív webfejlesztés kurzus. Öt leckén át egy működő alkalmazást építünk fel: a
**Feladatbank**ot, ami matekfeladatokat listáz, keres és tárol.

Minden lecke egy labor: elolvasod, közben írod a kódot, a végén van valami, ami működik.
Utána kapsz egy önálló feladatot, amit a saját ötleted szerint csinálsz meg.

## Kinek szól?

Neked, ha már programoztál valamilyen nyelven (változó, ciklus, függvény, tömb nem újdonság),
de a web világa még nem ismerős.

## Mit fogsz használni?

- [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) és [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS): az oldal szerkezete és kinézete
- [Tailwind CSS](https://tailwindcss.com/): CSS keretrendszer, amivel sokkal gyorsabb a stílusozás
- [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript) és [TypeScript](https://www.typescriptlang.org/): a böngészőben futó logika
- [Bun](https://bun.sh/): ez futtatja a kódot a böngészőn kívül, és ez kezeli a külső könyvtárakat
- [Express](https://expressjs.com/) és [SQLite](https://www.sqlite.org/): a saját szerverünk és adatbázisunk
- [React](https://react.dev/): a legelterjedtebb frontend könyvtár
- [Git](https://git-scm.com/) és [GitHub](https://github.com/): verziókövetés, ezen keresztül dolgozol

Mindegyikhez megkapod a telepítési lépéseket, amikor sorra kerül.

## Leckék

| #   | Lecke                                                      | Mit építünk                                        |
| --- | ---------------------------------------------------------- | -------------------------------------------------- |
| 01  | [HTML, CSS, Tailwind](leckek/01-html-css-tailwind/)        | A Feladatbank oldala, statikusan                   |
| 02  | [JavaScript, TypeScript](leckek/02-javascript-typescript/) | A kártyák adatból generálódnak, kereső és számláló |
| 03  | Webes kommunikáció, fetch                                  | Az adat már nem a kódban van, hálózatról jön       |
| 04  | Backend: REST API és adatbázis                             | Saját szerver és adatbázis a Feladatbank mögé      |
| 05  | React bevezetés                                            | Az egész frontend újraírva Reactben                |

A leckék egymásra épülnek, de **nem függenek egymástól**: minden leckének saját `1-start/`
mappája van, ami tartalmazza az előző lecke végeredményét. Ha kihagysz egyet, vagy nem
fejezted be, a következőt akkor is el tudod kezdeni.

## Hogyan használd?

1. **Forkold** ezt a repót a saját GitHub fiókodba (jobb felül a `Fork` gomb).
2. **Klónozd** le a forkot a gépedre.
3. Olvasd el a [SETUP.md](SETUP.md)-t, és állítsd be a fejlesztői környezeted.
4. Kezdd a [01-es leckével](leckek/01-html-css-tailwind/).
5. A saját munkádat **commitold** és **pushold** a forkodba. Így bármikor visszanézhető,
   mit csináltál, és ha elakadsz, meg tudod mutatni valakinek.

Dolgozz nyugodtan a `1-start/` mappákban, az a tiéd, azt írd át.

## Hogyan tanulj?

- Ne csak olvasd a kódot: **írd be, futtasd, rontsd el, és nézd meg mi történik.** A "mi
  történik, ha ezt kiveszem" kérdés többet tanít, mint három elolvasott bekezdés.
- Ne ugord át az önálló feladatot. A lecke lépései megmutatják, hogyan kell; a feladat az,
  ahol kiderül, hogy tudod is.
- **Kérdezz.** Googletől, AI-tól, egymástól, tőlünk.
- Az AI modellek egyre jobbak a kódolásban, de kezeld fenntartásokkal: időnként hülyeségeket képesek hihetően előadni.  
  Légy kritikus, kérdezz vissza, keress magyarázatot. 
- A legjobb forrás a dokumentáció, és ezt meglepően kevesen tudják. Leckénként a végén
  megtalálod a relevánsakat.

## Kapcsolódó anyag

Ez a kurzus a [Mök IT tudásbázisra](https://mok-it.github.io/) épül. Ott több elméleti
részlet és további témakör is megtalálható, ha valamiben mélyebbre akarsz menni.
