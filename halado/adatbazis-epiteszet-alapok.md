# Az adatbázis-építészet alapjai – Kapcsolatok és konzisztencia

Az adatbázis tervezése nem csupán technikai feladat, hanem stratégiai döntés is: a **helyes építészet** az alapja minden hatékony, bővíthető és biztonságos alkalmazásnak.

## 1. Miért fontos az építészet?

- **Struktúra ad az adatoknak**: Segít átláthatóan kezelni a tárolt információkat.
- **Későbbi optimalizálás alapja**: Egy jól megtervezett séma lehetőséget ad a gyors lekérdezésekre és a könnyű módosításokra.
- **Karbantarthatóság**: Egy átlátható struktúra hosszú távon csökkenti a hibák lehetőségét.
- **Konzisztencia**: Csak megfelelő kapcsolatokkal és megszorításokkal garantálható, hogy az adatok mindig helyesek maradnak.

## 2. Kapcsolatok tervezése

- Minden tábla legyen egyértelműen azonosítható (primary key).
- A **kapcsolatok** (foreign key-ek, junction/csatoló táblák) határozzák meg, hogyan “beszélgetnek” egymással az adatok.
- **Kapcsolati típusok**:
  - Egy-a-sokhoz (1:N)
  - Sok-a-sokhoz (N:M), junction táblákkal
  - Egy-az-egyhez (1:1)
- Mindig gondold végig, melyik kapcsolat mire szolgál, és milyen megszorításokat igényel.
  /Egy megjegyzés, hogy a modern SQL tervezésben az 1:1 kapcsolatot NEM használjuk olyan formában, hogy "beszúrjuk" más tábla elsődleges kulcsát.
  Tudom, én is hallottam olyat, hogy "ha laza kapcsolat kell": NEM. Mindig megszorítással idegen kulcsot delkalarálunk./
## 3. Konzisztencia és megszorítások

- **Külső kulcsok (foreign key):** Biztosítják, hogy csak létező rekordokra hivatkozunk.
- **ON DELETE/UPDATE szabályok:** CASCADE, RESTRICT, SET NULL – mindig mérlegeld, melyiket válaszd az adatok biztonsága érdekében!
- **Normalizáció:** Segít elkerülni az adatduplikációt és a felesleges redundanciát.
- **Egyedi megszorítások:** UNIQUE, CHECK, NOT NULL – ezek mind növelik az adatok minőségét.

## 4. Helyes "nyelvtan" – örök érvényű igazságok

Néhány szóban a helyes „szintaxisról”, amit magam is alkalmazok, és nekem bevált (Viescas és Hernandez tanárok tanácsai alapján):

- **Táblák neve:** Mindig többesszám.  
  Képzeld el ezt úgy, mint egy osztályt, aminek az egyedei lesznek az abban definiált rekordok.
- **Mezők neve:** Mindig egyes szám.  
  Ha olyannal találkozol, hogy például `telefonszámok`, az sosem helyes, inkonzisztens adatra utal.  
  Egy mező = egy adat. Szigorúan, sosem több.  
  Helyes példák: `mobil_szám`, `otthoni_szám`, `munkahelyi_szám`.
- **Többes mező soha!**  
  Ha több adatot kell tárolni (pl. több telefonszámot egy személyhez), akkor junction/kapcsoló táblát használj.
- **NF3 feltétel:** 1 mező = 1 adat.  
  Ettől nem érdemes eltérni, ez a konzisztencia alapja!
- **Névkonvenció:**  
  Mezők és táblák neveit mindig kisbetűvel definiáld, szóköz helyett `_` karaktert használj.

## 5. Magyar ékezetes karakterek, kódolás

Ez sajnos nagyon aktuális téma: magam is belefutottam, hogy nem UTF8 kódolású volt az adatbázis, és ezért hibákat okozott.

**Javaslat:**  
Ha tudod, hogy magyar ékezetes adattal kell dolgozni, érdemes eleve úgy létrehozni az adatbázist, hogy az **UTF8** kódolást használjon.

---

_Ez a magyarázat összefoglalja az adatbázis-építészet legfontosabb alapelveit, amelyekre minden további haladó téma – például optimalizálás vagy tranzakciókezelés – épül!_
