# Tranzakciós izolációs szintek – röviden, érthetően

Igyekszem egyszerűen megosztani veletek, amit jómagamnak sikerült megérteni erről a témáról. Ígérem, nem bonyolítom túl,
és semmiféle "szóvirágokat" sem használok az érthetőség érdekében.

## 1. UNREAD COMMITTED

Ez a legegyszerűbb izolációs szint, **erősen ajánlott mellőzni** az alábbi okok miatt:
- Itt a leggyakoribb a "piszkos olvasás" (dirty read).  
- Ez azt jelenti, hogy a tranzakció futása során olvashat olyan adatokat, amiket más tranzakciók már módosítottak, de még nem committálta, ezért ezek inkonzisztensek lehetnek.
- Példa:  
  Ha a tranzakció olvassa, hogy Tóth Norbert számlaegyenlege 1.236.000 Ft, és utal róla 658.000 Ft-ot, miközben egy másik tranzakció már levont 1.321.000 Ft-ot,
  a számla mínuszba kerülhet. Ez az abszolút "piszkos olvasás", amely megelőzhető lenne például a SERIALIZABLE izolációs szint beállításával.
- **Pénzügyi adatokhoz** kizárólag a SERIALIZABLE izolációs szintet használjuk!

## 2. READ COMMITTED

Ez a legtöbb adatbázisban **alapértelmezett** izolációs szint, de tranzakciót írva, biztonságos gyakorlat az elején külön definiálni.
- Kereskedelmi és nem kritikus tranzakciókat végző adatbázisokban általában bőven elegendő.
- Előnye: csak **committált adatokat enged olvasni/módosítani**, nem lassítja az adatbázist, nem zárol túlzottan.
- **Hátrány:** még előfordulhat a "megismételhetetlen olvasás" és "fantom sorok" problémája.

## 3. REPEATABLE READ

- Itt már **kizárható a "megismételhetetlen olvasás"** probléma, mert a zárolás nem engedi módosítani a zárolt adatokat más tranzakciónak.
- Érthetőbben: a tranzakció olvas egy adatot, majd később ugyanazt az adatot olvassa ismét, és biztosan ugyanazt kapja vissza, még ha közben más tranzakciók próbálnák is módosítani.
- Ezért banki, pénzügyi, tehát kritikus rendszerekben nem használunk olyan izolációs szintet, ami ezt a lehetőséget meghagyná.

## 4. SERIALIZABLE

A **legszigorúbb izolációs szint**.
- Az adatbázis úgy zárolja az ezzel a szabállyal érintett adatokat a tranzakció során, hogy más tranzakciók **sem olvashatják, sem írhatják** azokat a zárolás alatt.
- Előnye: teljesen kizárja a piszkos olvasást, a megismételhetetlen olvasást, illetve a "fantom sorok" problémákat.
- **Hátrány:** jelentősen lassítja az adatbázis működését, mert kizárja a tranzakciók párhuzamos futását.
- **"Fantom sorok" probléma:** amikor a tranzakció futása során, más tranzakciók által létrehozott új adatokat lát és olvas, amelyek előzőleg nem voltak ott.

---

_Ezeket az izolációs szinteket érdemes tudatosan alkalmazni – minden adatbázis céljától és kritikus szintjétől függően!_
