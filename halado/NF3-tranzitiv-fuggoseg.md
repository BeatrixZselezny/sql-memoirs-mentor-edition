# Tranzitív függőség – az “ALIEN” a tábládban

A tranzitív függőség az adatbázis-tervezés egyik legtrükkösebb, mégis legfontosabb fogalma – és a harmadik normálforma (NF3) lényege is egyben.

## Analógia: Az “ALIEN” a táblában

Amikor egy tábla tartalmaz egy olyan adatot, ami “idegen test” ott – azaz hivatalosan, az adatbázis logikája szerint nem is kéne ott lennie –, akkor **tranzitív függőséget** hoztunk létre.

**Szemléletesen:**  
Ez az “ALIEN”. Egy idegen, aki “ott van”, annak ellenére, hogy hivatalosan az adatbázis szerint NEM kéne, hogy ott legyen.

Ez akkor fordul elő, ha _nem normál forma szerint_ történik a kapcsolat létrehozása:  
- Nem idegen kulccsal kapcsoljuk a táblákat  
- Egyszerűen csak “bemásoljuk” egy másik tábla elsődleges kulcsát, de megszorítások és idegen kulcs deklarációk nélkül  
- Így az adat nem kontrollált, nem védett – és “idegenként” viselkedik a táblában

## Miért baj ez?

Az ilyen “ALIEN” adatok miatt:
- Redundancia, inkonzisztencia, hibás adatok jelennek meg
- Nem lehet garantálni az adatbázis integritását
- Később nehéz karbantartani, módosítani az adatokat

## Példa

Tegyük fel, hogy van egy “Rendelés” tábla, és minden rendeléshez tárolunk egy “Ügyfélváros” mezőt úgy, hogy azt egyszerűen bemásoljuk az “Ügyfél” táblából, de nincs idegen kulcs, nincs kapcsolat.  
Ha az ügyfél később költözik, az “Ügyfélváros” mező nem frissül automatikusan – így egy idegen, “alien” adat marad a táblában.

## Tanulság

A tranzitív függőség mindig “alienként” jelenik meg a táblában.  
Az NF3 (harmadik normálforma) célja: **távolítsuk el ezeket az alieneket!**  
Minden adatot csak ott tároljunk, ahol logikailag, adatbázis szinten is helye van – idegen kulcsokkal, helyes kapcsolatokkal.

---

_Ezt az analógiát és megértést Viescas és Hernandez tanárok gondolatai alapján dolgoztam ki. Nekem segített, remélem neked is! / Az ALIEN analógia persze
a sajátom :-) /_
