# SQL Halmazműveletek Cheat Sheet

## 1. UNION
- **Mit csinál?**  
  Két lekérdezés találatait egyesíti, az ismétlődéseket kiszűri (tehát minden rekord csak egyszer jelenik meg).
- **Mikor használd?**  
  Ha bármelyik lekérdezés eredménye érdekel, de a duplikátumok nem.
- **Analógia:**  
  Halmazok uniója (matematikai ∪ jel), vagy logikai OR (vagy).
- **Példa:**
  ```sql
  SELECT name FROM table1
  UNION
  SELECT name FROM table2;
  ```

---

## 2. INTERSECT
- **Mit csinál?**  
  Csak azokat adja vissza, amelyek mindkét lekérdezés eredményében szerepelnek.
- **Mikor használd?**  
  Ha a közös elemeket keresed a két eredményhalmazból.
- **Analógia:**  
  Halmazok metszete (matematikai ∩ jel), vagy logikai AND (és).
- **Példa:**
  ```sql
  SELECT name FROM table1
  INTERSECT
  SELECT name FROM table2;
  ```

---

## 3. EXCEPT
- **Mit csinál?**  
  Az első lekérdezés eredményeiből kivonja a másodikét (csak azokat adja vissza, amik az elsőben vannak, de a másodikban nincsenek).
- **Mikor használd?**  
  Ha csak az első halmaz „egyedi” elemeire vagy kíváncsi.
- **Analógia:**  
  Halmazok különbsége (matematikai \ jel), vagy logikai NOT (nem).
- **Példa:**
  ```sql
  SELECT name FROM table1
  EXCEPT
  SELECT name FROM table2;
  ```

---

## További tudnivalók:
- Mindhárom műveletnél a SELECT-eknek **ugyanannyi oszlopot** kell visszaadniuk, **azonos típusban és sorrendben**!
- Az összes eredményre igaz: **nincs sorok sorrendje** (ha kell, használj `ORDER BY`-t).
- Az **UNION ALL** változat _nem szűri ki_ a duplikációkat!
