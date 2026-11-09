# Önálló feladat: adatvezérelt lista

Az előző lecke feladatában csináltál egy saját oldalt. Most keltsd életre: az elemek adatból
jöjjenek, és lehessen köztük keresni. Ha akkor kihagytad, válassz most témát:

- Egy filmes vagy könyves lista, műfajokkal
- Receptek, hozzávalók és elkészítési idő szerint
- Együttesek vagy albumok
- Túraútvonalak, hosszal és nehézséggel
- _Bármi más, aminek listája van_

## Követelmények

- [ ] Minden megjelenő elem egy adattömbből jön, egy sincs kézzel beírva a HTML-be
- [ ] A kártya markupja egy [`<template>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/template)
      elemben van, és egy függvény klónozza és tölti ki adatból
- [ ] A szövegeket `textContent`-tel írod be
- [ ] Van kereső, ami **gépelés közben** szűr
- [ ] Ha semmi nem felel meg a szűrésnek, értelmes üzenet jelenik meg, nem üres képernyő
- [ ] A kód [TypeScriptben](https://www.typescriptlang.org/) van
- [ ] Van `type` az adat alakjára
- [ ] Nincs típushiba
- [ ] A kinézet továbbra is [Tailwinddel](https://tailwindcss.com/) készül

## Amiben tovább mehetsz

Ezek nem kötelezőek, de ha van kedved:

- Csinálj egy űrlapot, amivel új elemet lehet felvenni a listába
- Őrizd meg a listát oldalfrissítés után a
  [localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)-ban
- Kattintásra nyíljon le az elem részletes nézete
