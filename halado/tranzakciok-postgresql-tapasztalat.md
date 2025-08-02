# Tranzakciók világa – PostgreSQL gyakorlati tapasztalat

Mestervizsgára készülve, kihagyhatatlan tanulás és edzés a **tranzakciók** témaköre, amiben azóta meglehetősen elmélyedtem – és bevallom, szerelem lett a részemről :-)

Nyilván mindenkinek van, lesz SQL-ben olyan technika vagy téma, ami különösen kedves. Nekem az egyik az NF3 normalizációs tervezés, a másik pedig a tranzakció.

## Küzdelmes tapasztalat – okulásképpen

Volt egy igazán küzdelmes, tanulságos élményem a tranzakciókkal kapcsolatban, amit megosztok veletek, hátha segít eligazodni abban az informális káoszban, amiben én is bolyongtam.

Az elején úgy döntöttem, hogy az adatbázisomban a táblák **ON DELETE CASCADE** megszorításokkal lettek deklarálva. Utóbb kiderült: nem is olyan jó ötlet, mert a lépcsőzetes törlés egy hibás döntés folytán nagyon komoly adatveszteséget eredményezhet – tehát nem túl biztonságos.

Oké, át kellett szervezni a sokkal biztonságosabb **ON DELETE RESTRICT** megszorításra, méghozzá kilenc tábla esetében. Gondoltam, soha jobb alkalom, hogy írjak erre egy szép és biztonságos tranzakciót!

### A kezdő tervező rémálma

Itt kezdődött minden kezdő tervező rémálma:  
- Az egyik tanács: írjam meg raw SQL kódként.  
- A másik: “Á, azt ne! Írd meg DO blokkban, ott van hibakezelés és biztonságos!”  
- Különböző **SAVEPOINT**-ekkel és **ROLLBACK TO SAVEPOINT**-ekkel kavartak, aztán kiderült:  
  - PostgreSQL-ben DDL műveleteknél ez nem támogatott, nem valósították meg.  
  - Ha jobban megnézed, teljesen szembemenne az ACID elvekkel.

A végére megértettem – de addig eltelt meló mellett két hét, és már égnek állt a hajam a káosztól.

### Végül a nagy tanulság

Kikötöttem ott: **no SAVEPOINT**. Írd meg lineárisan, start és imádkozz.  
És ekkor jött a "nagy elefánt": **PostgreSQL** – és megmutatta az igazi természetét.

- Elindítottam a tranzakciót.
- Néhány helyen elírtam a megszorítások neveit, pár DDL nem ment át, de a többi igen.
- Végül egy automatikus **ROLLBACK**-et kaptam a nagy Elefánttól, minden konzisztens maradt – én pedig csak ültem, és tátottam a számat.

Akkor értettem meg, hogy nekem **NEM kell manipulálni SAVEPOINT-ekkel**, mert a PostgreSQL hibátlanul ledelegálja, és full ACID a vége.

Így lett ebből szerelem a nagy elefánttal :-)  
Fantasztikus szinten leveszi a fejlesztőről a stresszt a PostgreSQL, azt gondolom.

A hibákat egy config táblába küldtem, percek alatt átírtam, és lement minden DDL-em.  
Számomra nagyon tanulságos volt látni az ACID igazi természetét és erejét.

---

_Ezt a tapasztalatot gyakorlati tanulás közben szereztem, remélem segítséget ad a tranzakciók mester szintű megértéséhez!_
