Kryptex HUF Profitability

Tampermonkey-script, amely a [Kryptex Hardware dashboard](https://www.kryptex.com/site/hardware) eurós jövedelmezőségi adatai alatt megjeleníti a magyar forintra (HUF) átszámított összegeket, a Magyar Nemzeti Bank (MNB) hivatalos árfolyamával.

A forintos sor az eredeti eurós sor stílusát használja, azonos betűmérettel, betűvastagsággal és színnel.

## Megjelenés

Példa **400 Ft/EUR szemléltető árfolyammal**:

```text
€1000.00/mo · €32.26/d
400 000,00 Ft/hó · 12 904,00 Ft/nap
```

Az összegek magyar számformátummal, két tizedesjeggyel jelennek meg. A script állapotüzenetei és az egérrel megjeleníthető árfolyam-információk is magyar nyelvűek.

## Funkciók

- Automatikusan elindul a Hardware dashboard betöltésekor.
- Az eurós összegek megtartása mellett megjeleníti a forintos értékeket.
- Követi a dashboard eurós adatainak változását.
- A legutolsó közzétett EUR/HUF árfolyamot közvetlenül az [MNB hivatalos napi árfolyamtáblázatából](https://www.mnb.hu/arfolyamok) olvassa ki.
- Helyben menti az árfolyamot, és a nyitott oldalon frissítést kér, ha az utolsó letöltés óta legalább egy óra eltelt.
- A forintos sor fölé vitt egérrel megmutatja az árfolyam értékét és dátumát.
- Sikertelen lekérdezéskor figyelmeztetés mellett tovább használja a legutóbb mentett árfolyamot.

## Követelmények

- Microsoft Edge, telepített [Tampermonkey](https://www.tampermonkey.net/) bővítménnyel.
- Engedély a felhasználói scriptek futtatására és a Kryptex oldal elérésére.
- Bejelentkezett Kryptex-fiók, a Hardware dashboardon EUR-ban megjelenített, `€…/mo · €…/d` formátumú összegekkel.

A script Edge és Tampermonkey használatához készült. Más böngészőkkel és scriptkezelőkkel a működés nincs ellenőrizve.

## Telepítés

1. Telepítsd a Tampermonkey bővítményt Edge-ben.
2. Nyisd meg az `edge://extensions` oldalt, és engedélyezd a **Fejlesztői módot**, vagy a bővítmény beállításainál a **Felhasználói szkriptek engedélyezése / Allow User Scripts** kapcsolót, ha elérhető. Az F12-es fejlesztői eszközök megnyitása önmagában nem engedélyezi a scripteket. Segítség: [Tampermonkey engedélyezési útmutató](https://www.tampermonkey.net/faq.php?q=Q209).
3. Nyisd meg a repóban a [kryptex-mnb-huf.user.js](kryptex-mnb-huf.user.js) fájlt, és másold ki a teljes tartalmát. GitHubon használd a **Raw** nézetet vagy a másolás gombot.
4. A Tampermonkey menüjében válaszd az **Új script létrehozása / Create a new script** lehetőséget.
5. Töröld az összes alapértelmezett kódot, és illeszd be a kimásolt scriptet. Mentsd **Ctrl+S**-sel.
6. Ellenőrizd, hogy a script engedélyezve van, majd töltsd újra a Kryptex Hardware dashboardot.
7. Ha a Tampermonkey engedélyt kér az `www.mnb.hu` eléréséhez, engedélyezd.

A legelső sor pontosan ez maradjon:

```js
// ==UserScript==
```

## Működés

A script megkeresi a dashboard azon `.hwt-meta` elemeit, amelyek eurós havi és napi összegeket tartalmaznak. A két összeget külön-külön átszámítja, és egy forintos sort illeszt alájuk. Átveszi az eredeti sor stílusát, és figyeli az oldal változásait, hogy a forintos értékek is frissüljenek.
Az árfolyamot az MNB weboldalának napi HTML-táblázatából olvassa. Nem használja a SOAP-végpontot, és nem vesz igénybe külső devizaárfolyam-szolgáltatót. Mindig a legutolsó közzétett árfolyammal számol, ezért annak dátuma például hétvégén vagy ünnepnapon korábbi lehet a mai napnál.
Az átszámítás alapja a Kryptex által már kerekítve megjelenített eurós összeg. A script nem készít külön jövedelmezőségi becslést, és nem számol devizaváltási díjakkal.

## Adatkezelés és jogosultságok

A script a megjelenített eurós összegeket helyben olvassa. Nem küld jövedelmezőségi adatokat, fiókadatokat vagy belépési adatokat az MNB-nek. Az árfolyamot anonim GET-kéréssel tölti le a `https://www.mnb.hu/arfolyamok` címről.
A Tampermonkey tárhelyén csak az árfolyamot, a közzétételi dátumot és a letöltés időpontját menti. Nem tartalmaz analitikát vagy követőkódot, és nem módosítja a fiókbeállításokat vagy a kifizetéseket.
Független közösségi script, amely nem áll kapcsolatban a Kryptexszel vagy az MNB-vel.
