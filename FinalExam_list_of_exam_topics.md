# Programtervező informatikus BSc államvizsga tételsor
## Tematika
*Módosítva: 2025. március 20.*

---

## Számításelméleti tárgycsoport

### 1. Reguláris nyelvek
Definiálása reguláris kifejezéssel, felismerése véges automatákkal.  
Ezen eszközök ekvivalenciája: NFA → DFA átalakítás, reguláris kifejezés → NFA konstruálás az automaták által elfogadott nyelvek zártsági tételei alapján.

**Témakörök**
- Halmazokkal kapcsolatos definíciók
- Descartes-szorzat
- Relációk és típusaik
- Halmazok számossága
- Zártság fogalma és meghatározása
- Skatulya elv
- Diagonalizálási elv
- Nyelvek definíciója
- Műveletek nyelvekkel
- Reguláris nyelvek osztálya
- Reguláris kifejezések
- Véges automaták
- Ekvivalencia: NFA → DFA, reguláris kifejezés → NFA

**Irodalom**
- A digitális számítás elmélete tárgy oktatási segédanyagai
- Harry R. Lewis, Christos H. Papadimitriou: *Elements of the Theory of Computation*, 1–2. fejezet

---

### 2. Környezetfüggetlen nyelvek
Definiálásuk környezetfüggetlen nyelvtannal, felismerésük veremautomatával.  
Ekvivalencia: CFG → PDA konstruálás, zártsági tételek.

**Témakörök**
- Környezetfüggetlen nyelvek definíciója
- Egylépéses származtatás
- Környezetfüggetlen vs. környezetfüggő nyelvek
- Nyelvtan fogalma
- Speciális nyelvtanok
- Reguláris vs. környezetfüggetlen nyelvtan
- Második pumpálási tétel
- Veremautomata fogalma
- Egyszerű veremautomata
- CFG → PDA konstruálás
- Zártsági tulajdonságok

**Irodalom**
- A digitális számítás elmélete tárgy oktatási segédanyagai
- Lewis–Papadimitriou: *Elements of the Theory of Computation*, 3. fejezet

---

### 3. Turing elfogadható nyelvek

**Témakörök**
- Turing-gép definíciója
- Turing-gép vs. veremautomata
- Végállapot vs. megállási állapot
- Turing-gép kimenete
- Elemi machine schemák
- Másoló gép
- Shifting (shiftelő) gép
- aⁿbⁿcⁿ nyelvet eldöntő gép
- Karakterisztikus függvény
- Church–Turing tézis
- Megállási probléma
- Turing-elfogadható és eldönthető nyelvek
- Kapcsolatuk

**Irodalom**
- A digitális számítás elmélete tárgy oktatási segédanyagai
- Lewis–Papadimitriou: *Elements of the Theory of Computation*, 4. fejezet

---

### 4. Algoritmus futási ideje, rendezés és keresés

**Témakörök**
- Aszimptotikus jelölések
- Legjobb, legrosszabb, átlagos futási idő
- Kupacrendezés
- Gyorsrendezés
- Buborékrendezés
- Minimum kiválasztásos rendezés
- Közvetlen kiválasztásos rendezés
- Beszúró rendezés
- Összefésülő rendezés
- Leszámláló rendezés
- Számjegyes rendezés
- Edényrendezés
- Lineáris keresés
- Bináris keresés

**Irodalom**
- Adatstruktúrák és algoritmusok oktatási segédanyagok
- Cormen et al.: *Új algoritmusok*
- Fekete et al.: *Algoritmusok és adatszerkezetek*

---

### 5. Elemi és fejlett adatszerkezetek

**Témakörök**
- Verem, sor
- Láncolt listák: egyszeres, kétszeres, cirkuláris, fejelemes
- Bináris keresőfák
- Kupacok
- Piros-fekete fák
  - Tulajdonságok
  - Fekete-magasság
  - Forgatások
  - Beszúrás, törlés
- B-fák
  - Definíció
  - Magasság
  - Beszúrás, törlés
- Hasító táblák
  - Hasító függvények
  - Láncolás
  - Nyílt címzés
  - Lineáris, négyzetes kipróbálás
  - Dupla hasítás

---

### 6. Gráfalgoritmusok

**Témakörök**
- Gráfábrázolás
  - Szomszédsági lista
  - Szomszédsági mátrix
- Mélységi keresés (DFS)
- Szélességi keresés (BFS)
- Minimális feszítőfa
  - Prim algoritmus
  - Kruskal algoritmus
- Legrövidebb utak
  - Körmentes gráf
  - Bellman–Ford
  - Dijkstra
- Maximális folyam
  - Ford–Fulkerson algoritmus
- Futási idők elemzése

---

### 7. Redundancia és normalizálás adatbázisokban

**Témakörök**
- Redundancia problémája
- Anomáliák
- Funkcionális függőségek
  - Teljes
  - Részleges
  - Tranzitív
- Normalizálás
  - 0NF
  - 1NF
  - 2NF
  - 3NF
  - BCNF
- Relációs vs. NoSQL adatmodell
- ACID elvek
- CAP tétel
- Skálázhatóság
- Konzisztenciamodellek
- NoSQL rendszerek típusai
- MapReduce paradigma

---

### 8. Koncepcionális adatbázistervezés

**Témakörök**
- ER modell
  - Erős és gyenge egyedek
  - Attribútumok
  - Kapcsolatok
  - Kardinalitás
- EER modell
  - Specializáció
  - Általánosítás
  - Unió típus
- Leképezés relációs modellre
- Relációs algebra
- SQL
  - DML utasítások
  - Lekérdezések
  - Kapcsolat relációs algebrával

---

### 9. Ágensek és ítéletkalkulus

**Témakörök**
- Ágens fogalma
- Feladatkörnyezet
- Környezetek tulajdonságai
- Ágenstípusok
- Multiágens rendszerek
- Logikai ágens
- Ítéletkalkulus
  - Szintaktika
  - Szemantika
  - Logikai következmény
- Tételbizonyítás
  - Igazságtábla
  - Quine algoritmus
  - Formális levezetés
  - Rezolúció

---

### 10. Problémareprezentáció és keresés

**Témakörök**
- Állapottér gráffal és fával
- Vak keresések
  - BFS
  - DFS
  - Korlátozott mélység
  - Iteratívan mélyülő DFS
  - Egyenletes költségű keresés
- Heurisztikus keresés
  - Mohó keresés
  - A*
  - IDA*
  - RBFS
- Lokális keresések
  - Hegymászás
  - Szimulált lehűtés
- Populációs keresések
  - Nyaláb keresés
  - PSO
  - Genetikus algoritmus
- Kétszemélyes játékok
  - Minimax
  - Alfa-béta vágás

---

### 11. Gépi tanulás és neurális hálók

**Témakörök**
- Gépi tanulás fajtái
  - Felügyelt
  - Nem felügyelt
  - Félig felügyelt
  - Megerősítéses
- Tanulás folyamata
- Túltanulás
- Döntési fák
- K-means
- Neurális hálók
  - Neuron modell
  - Aktivációs függvények
  - Háló felépítése
  - Tanítás
  - Veszteségfüggvények
  - Regularizáció
  - Mélytanulás

---

## Informatikai tárgycsoport

### 1. Információ reprezentációja
- Számrendszerek
- Endianitás
- Fix- és lebegőpontos ábrázolás
- Hamming-kód

### 2. ALU felépítése
- Univerzális teljesség
- Összeadó áramkörök
- Kivonó áramkörök
- Szorzás
- Osztás

### 3. Vezérlő egységek
- Huzalozott vezérlés
- Mikrokódos vezérlés
- Mealy- és Moore-modellek
- Horizontális és vertikális mikrokód

### 4. Folyamatkezelés
- Folyamat fogalma
- Multiprogramozás
- Állapotok és átmenetek
- Ütemezési algoritmusok
- Szinkronizáció
- Szemafor
- Kritikus szakasz
- Holtpont

### 5. Tárkezelés
- Memóriahierarchia
- Virtuális memória
- Lapozás
- Szegmentálás
- Lapcsere algoritmusok

### 6. Háttértárak és állománykezelés
- Merevlemez felépítése
- RAID
- Állomány allokáció
- Elosztott állománykezelés

### 7. Fizikai és adatkapcsolati réteg
- Átviteli közegek
- Topológiák
- Keretszerkezet
- MAC cím
- Switch működés

### 8. Hálózati réteg
- IPv4 és IPv6
- Publikus és privát címek
- VLSM
- Alhálózat számítás
- Irányítóprotokollok

### 9. Szállítási réteg
- TCP és UDP
- Portok
- TCP kapcsolat felépítése
- Megbízhatóság
- Csúszóablak

### 10. Szoftvertechnológia
- Szoftver mint termék
- Fejlesztési modellek
- Vízesés
- Iteratív
- Inkrementális
- XP
- Spirális modell

### 11. Objektumorientált tervezés
- OOA, OOD, OOP
- UML diagramok
- RUP
  - Fázisok
  - Diszciplinák

### 12. Szoftvertesztelés
- Verifikáció
- Validáció
- Lefedettség
- Fekete- és fehérdoboz tesztelés
- Tesztelési szintek
- Teszttervezési technikák
