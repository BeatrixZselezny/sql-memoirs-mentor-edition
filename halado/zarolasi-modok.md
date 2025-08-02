# Zárolási módok – UPDATE SHARED & UPDATE EXCLUSIVE

Az adatbázis tranzakciók során különböző zárolási módokat alkalmazunk az adatok integritásának biztosítása érdekében. Ezek közül kettő, az **UPDATE SHARED** és az **UPDATE EXCLUSIVE** zárolás, különösen fontosak lehetnek, amikor többen szeretnének módosítani vagy olvasni ugyanazt az adatot.

## UPDATE SHARED

- Több tranzakció kérhet UPDATE SHARED zárolást ugyanarra az adatra.
- Lehetővé teszi, hogy többen “előre jelezzék” a szándékukat az adat módosítására, de tényleges írás csak az EXCLUSIVE zárolás megszerzése után lehetséges.
- Nem blokkolja a többi olvasót, és azokat sem, akik szintén UPDATE SHARED zárolást kérnek.

## UPDATE EXCLUSIVE

- Egyetlen tranzakció szerezheti meg ezt a zárolást egy adott adaton/táblán.
- Az UPDATE EXCLUSIVE zárolás megszerzése után csak az adott tranzakció módosíthatja az adatot, másoknak várniuk kell.
- Teljes biztonságot ad az adat módosításához, garantálja a konzisztenciát.

## Dead lock – zárolási sorrend fontossága

**Nagyon fontos a helyes zárolási sorrend, a dead lock probléma elkerülése érdekében!**

- **Dead lock** akkor lép fel, amikor két (vagy több) tranzakció egymásra vár:
    - Például: A tranzakció vár B-re, hogy felszabadítson egy zárolt adatot, és fordítva.
- Ennek megelőzése érdekében **mindig azonos sorrendben zároljunk**.  
    - Példa: Ha A tranzakcióban zárolod a "vásárlók" tábla "Név" majd "Cím" oszlopát, B tranzakcióban is ebben a sorrendben zárolj!
- A modern adatbázisok érzékelik a dead lock versenyhelyzetet, és automatikusan megszakítják valamelyik tranzakciót,  
  **de fejlesztőként elengedhetetlen, hogy tisztában legyünk a helyes zárolási sorrenddel és menedzsmenttel!**

## Személyes megjegyzés

Amikor először találkoztam ezekkel a zárolási módokkal, meglepett, mennyire finoman hangolható az adatbázis viselkedése. Az EXCLUSIVE zárolás például garantálja, hogy senki más nem piszkálhatja az adott adatot, amíg a tranzakció zajlik – így minden módosítás biztonságosan végrehajtható.

---

_Ezeket a zárolási módokat és a helyes zárolási sorrendet érdemes ismerni, mert hatékonyan és biztonságosan lehet velük tranzakciókat kezelni, főleg nagyobb, párhuzamosan futó rendszerekben._
