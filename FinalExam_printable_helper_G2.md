# RÉSZLETES ZÁRÓVIZSGA KIDOLGOZÁS - PANNON EGYETEM MIK
**Forrás:** 250320-PI-BSc-zarovizsga-tematika-250320.pdf

---

# I. SZÁMÍTÁSELMÉLETI TÁRGYCSOPORT

## 1. Tétel: Reguláris nyelvek
**Téma:** Definíció reguláris kifejezéssel, véges automaták, ekvivalencia, zártság.

### 1.1 Halmazelméleti alapok
* **Descartes-szorzat:** $A \times B$ azon rendezett párok halmaza, ahol az első elem $A$-ból, a második $B$-ből való.
* **Skatulya-elv:** Ha $n$ elemet $m$ halmazba osztunk, és $n > m$, akkor legalább egy halmazba egynél több elem kerül. (Fontos a pumpálási lemma bizonyításához).
* **Diagonalizálási elv:** Cantor módszere a valós számok nem megszámlálható voltának bizonyítására (később a megállási problémánál fontos).

### 1.2 Reguláris nyelvek leírása
* **Reguláris kifejezések (RE):**
    * Elemi kifejezések: $\emptyset$ (üres halmaz), $\varepsilon$ (üres szó), $a$ (ábécé egy betűje).
    * Műveletek: Unió ($+$ vagy $\cup$), Konkatenáció ($\cdot$), Kleene-csillag ($*$: 0 vagy több ismétlés).
* **Véges Automaták:**
    * **DFA (Determinisztikus):** Minden állapotból minden bemeneti jelre pontosan egy átmenet van. $M = (Q, \Sigma, \delta, q_0, F)$.
    * **NFA (Nem-determinisztikus):** Egy állapotból egy jelre több állapotba is léphet, vagy léphet $\varepsilon$ (üres) átmenettel is bemenet olvasása nélkül.

### 1.3 Eszközök ekvivalenciája
A Kleene-tétel szerint a RE, DFA és NFA kifejezőereje azonos.
1.  **NFA $\to$ DFA átalakítás (Hatványhalmaz konstrukció):**
    * A DFA állapotai az NFA állapotainak részhalmazai.
    * Ha az NFA-nak $n$ állapota van, a DFA-nak legfeljebb $2^n$.
    * Kezdőállapot: Az NFA kezdőállapotának $\varepsilon$-lezártja (azok az állapotok, amik csak $\varepsilon$ lépésekkel elérhetők).
2.  **Reguláris kifejezés $\to$ NFA konstruálás:**
    * Induktív módon építjük fel.
    * Unió: Új kezdőállapotból elágazás a két automata felé.
    * Konkatenáció: Az első automata végállapotaiból $\varepsilon$-átmenet a második kezdőállapotába.
    * Csillag: Visszacsatolás a végállapotból a kezdőbe $\varepsilon$-nal.

### 1.4 Zártsági tételek
A reguláris nyelvek osztálya zárt a következőkre: Unió, Metszet, Komplementer, Konkatenáció, Kleene-csillag, Tükrözés, Homomorfizmus.  

---

## 2. Tétel: Környezetfüggetlen nyelvek (CF)
**Téma:** CF nyelvtan, Veremautomata, Pumpálási tétel.

### 2.1 Környezetfüggetlen nyelvtan (CFG)
* **Definíció:** $G = (V, \Sigma, P, S)$. A szabályok alakja $A \to \gamma$, ahol $A$ egy nemterminális (változó). A behelyettesítés nem függ a környezettől.
* **Származtatás:** Lépések sorozata a kezdőszimbólumból a terminális szóig.
    * *Baloldali:* Mindig a bal szélső nemterminálist fejtjük ki.
* **Szintaktisfa (Derivációs fa):** A származtatás grafikus ábrázolása. Ha egy szóhoz több különböző fa tartozik, a nyelvtan **kétértelmű**.

### 2.2 Veremautomata (PDA)
* Olyan véges automata, amelynek van egy végtelen méretű verme (LIFO).
* **Működés:** Az automata olvassa a bemenetet, és a verem tetején lévő szimbólum alapján dönt (push/pop).
* **CFG $\to$ PDA konstrukció:**
    * A veremben a várt szimbólumokat tároljuk.
    * Ha nemterminális van a tetőn: nem olvasunk bemenetet, hanem a veremben kicseréljük a nemterminálist a szabály jobb oldalára (tippelés).
    * Ha terminális van a tetőn: összehasonlítjuk a bemenettel (match).

### 2.3 Második pumpálási tétel (CF nyelvekre)
* Minden elég hosszú $z \in L$ környezetfüggetlen szó felbontható $z = uvwxy$ alakra úgy, hogy $|vx| \ge 1$, és $uv^iwx^iy$ is a nyelv része minden $i \ge 0$-ra. (Két részt pumpálunk egyszerre).
* Arra használjuk, hogy bizonyítsuk egy nyelvről, hogy **NEM** környezetfüggetlen (pl. $a^nb^nc^n$).

### 2.4 Zártság
* **Zárt:** Unió, Konkatenáció, Kleene-csillag, Tükrözés.
* **NEM zárt:** Metszet (két CF nyelv metszete lehet környezetfüggő), Komplementer.  

---

## 3. Tétel: Turing gépek
**Téma:** Turing gép, Machine Schema, Eldönthetőség, Church-Turing tézis.

### 3.1 Turing gép (TM)
* **Definíció:** Végtelen szalag, író-olvasó fej, véges vezérlő. Állapotátmenet: (Jelenlegi állapot, Olvasott jel) $\to$ (Új állapot, Írt jel, Fejmozgás L/R).
* **Megállás:** Külön *Elfogadó* ($q_{acc}$) és *Elutasító* ($q_{rej}$) állapot. Ha ide ér, a gép azonnal megáll.
* **Variációk:** Többszalagos TM (ekvivalens az egyszalagossal), Nem-determinisztikus TM (ekvivalens a determinisztikussal).

### 3.2 Machine Schema (Gépi sémák)
Összetett gépek építése elemi gépekből (Jobbra, Balra, Ír):
* **Másoló gép:** $w \# \to w \# w$.
* **Shiftelő gép:** Eltolja a szalag tartalmát.
* **$a^n b^n c^n$ felismerő:** Megkeres egy a-t, áthúzza, keres egy b-t, áthúzza, keres egy c-t, áthúzza. Ismétli, amíg el nem fogy.

### 3.3 Eldönthetőség és Elfogadhatóság
* **Church-Turing tézis:** Minden, ami algoritmikusan kiszámolható, az kiszámolható Turing-géppel is.
* **Turing-eldönthető (Rekurzív):** A gép minden bemenetre véges időn belül megáll (IGEN vagy NEM választ ad).
* **Turing-elfogadható (Rekurzívan felsorolható):** Ha a szó a nyelvben van, megáll és elfogad. Ha nincs benne, lehet, hogy végtelen ciklusba kerül.
* **Megállási probléma:** Adott program és bemenet esetén eldönthető-e, hogy a program megáll-e? Bizonyítottan **nem eldönthető** (de elfogadható).  

---

# II. ALGORITMUSOK ÉS ADATSZERKEZETEK

## 4. Tétel: Futási idő és Rendezések
**Téma:** Aszimptotika, Rendező és Kereső algoritmusok.

### 4.1 Aszimptotikus jelölések
* **$O(f(n))$:** Felső korlát. Az algoritmus legrosszabb esetben sem lassabb ennél (konstans szorzótól eltekintve).
* **$\Omega(f(n))$:** Alsó korlát.
* **$\Theta(f(n))$:** Pontos rend.

### 4.2 Rendező algoritmusok
* **Négyzetes $O(n^2)$:**
    * *Buborék:* Szomszédos csere.
    * *Beszúró (Insertion):* Kártyarendezés elv. Kicsi vagy majdnem rendezett tömbre nagyon gyors.
    * *Kiválasztó (Selection):* Minimum kiválasztása és előre helyezése.
* **Loglineáris $O(n \log n)$:**
    * *Gyorsrendezés (Quicksort):* Oszd meg és uralkodj. Vezérelem (pivot) választás. Átlagosan a leggyorsabb, de legrosszabb esetben $O(n^2)$. Helyben rendez.
    * *Összefésülő (Merge Sort):* Felezés, majd rendezett összefésülés. Stabil, de extra memóriát igényel.
    * *Kupacrendezés (Heapsort):* Kupac adatszerkezet építése ($O(n)$), majd a maximum (gyökér) cseréje az utolsó elemmel és süllyesztés ($O(n \log n)$).
* **Lineáris $O(n)$:**
    * *Leszámláló:* Ha az elemek kis egész számok.
    * *Edény/Vödör (Bucket):* Intervallumokba osztás.

### 4.3 Keresések
* **Lineáris:** $O(n)$, rendezetlen tömbben.
* **Bináris:** $O(\log n)$, rendezett tömbben. Felezéses módszer.  

---

## 5. Tétel: Adatszerkezetek
**Téma:** Listák, Fák, Hash.

### 5.1 Listák és alapok
* **Verem:** LIFO. Call stack-hez. Műveletek: Push/Pop.
* **Sor:** FIFO. Ütemezéshez. Műveletek: Enqueue/Dequeue.
* **Láncolt listák:**
    * *Egyszeresen:* Csak a következőre mutat.
    * *Kétszeresen:* Előre és hátra is mutat (törlés egyszerűbb).
    * *Fejelemes (Sentinel):* Technikai elem a lista elején/végén, hogy ne kelljen vizsgálni az üres listát külön.

### 5.2 Fák
* **Bináris Keresőfa (BST):** Keresőfa tulajdonság: Bal < Szülő < Jobb. Műveletek ideje a fa magasságától függ ($h$).
* **Kupac (Heap):** Teljes bináris fa, tömbben tárolva.
    * *Max-kupac tulajdonság:* Szülő $\ge$ Gyerekek.
* **Piros-Fekete fa:**
    * Önkiegyensúlyozó BST. Magassága garantáltan $O(\log n)$.
    * Szabályok: Gyökér fekete, levél fekete, pirosnak nem lehet piros gyereke, minden úton ugyanannyi fekete csúcs (fekete-magasság).
    * Helyreállítás: Átszínezés és Forgatás.
* **B-fa:**
    * Háttértárakhoz optimalizált, széles és lapos fa.
    * Egy csúcsban sok kulcs van. Minden levél azonos mélységben.

### 5.3 Hasító táblázatok (Hash)
* **Cél:** $O(1)$ átlagos elérési idő.
* **Hash függvény:** Kulcs $\to$ Index transzformáció.
* **Ütközéskezelés:**
    * *Láncolás:* Azonos indexű elemek egy láncolt listában.
    * *Nyílt címzés:* Ha a hely foglalt, újat keresünk (Lineáris próbálás, Négyzetes próbálás, Dupla hasítás).  

---

## 6. Tétel: Gráf algoritmusok
**Téma:** Bejárás, MST, Útvonal, Folyam.

### 6.1 Bejárások
* **Szélességi (BFS):** Sor adatszerkezet. Szintről szintre halad. Súlyozatlan gráfban legrövidebb utat ad.
* **Mélységi (DFS):** Verem/Rekurzió. Visszalépéses (backtrack) keresés.

### 6.2 Minimális Feszítőfák (MST)
Összefüggő gráf összes csúcsának összekötése minimális összsúllyal (kör nélkül).
* **Kruskal:** Élek növekvő sorrendben. Hozzáadjuk, ha nem okoz kört (Union-Find struktúrával).
* **Prim:** Egy pontból indul, mindig a legközelebbi csúcsot szippantja be a kész fába.

### 6.3 Legrövidebb utak
* **Dijkstra:** Csak nem-negatív élekre! Mohó algoritmus. Prioritási sorral választja a legközelebbi elérhető csúcsot.
* **Bellman-Ford:** Negatív élekre is működik. $V-1$-szer lazít minden élt. Ha utána is tud lazítani $\to$ negatív kör van.

### 6.4 Maximális folyam
* **Ford-Fulkerson:** Javítóutakat keres a maradék hálózatban (ahol van még szabad kapacitás), és növeli a folyamot.
* **Max-Flow Min-Cut:** A maximális folyam értéke egyenlő a hálózat minimális vágásának kapacitásával.  

---

# III. ADATBÁZIS-KEZELÉS

## 7. Tétel: Relációs modell és NoSQL
**Téma:** Normalizálás, Anomáliák, NoSQL típusok.

### 7.1 Relációs tervezés
* **Függőségek:**
    * *Funkcionális ($A \to B$):* A értéke meghatározza B-t.
    * *Tranzitív ($A \to B \to C$):* C csak B-n keresztül függ A-tól.
* **Anomáliák:** Redundancia miatt fellépő hibák (beszúrási, törlési, módosítási).
* **Normálformák (Normalizálás):**
    * *1NF:* Minden mező atomi (nem osztható), nincsenek ismétlődő csoportok.
    * *2NF:* 1NF + Nincs részleges függőség (összetett kulcs esetén minden nem-kulcs a *teljes* kulcstól függjön).
    * *3NF:* 2NF + Nincs tranzitív függőség.
    * *BCNF:* Minden determináns (ami meghatároz mást) jelölt kulcs legyen.

### 7.2 NoSQL és Big Data
* **CAP tétel:** Elosztott rendszerben a 3-ból csak 2 garantálható:
    * **C**onsistency (Konzisztencia - mindenki ugyanazt látja).
    * **A**vailability (Rendelkezésre állás - mindig van válasz).
    * **P**artition Tolerance (Partíciótűrés - hálózati szakadás esetén is működik).
* **NoSQL típusok:**
    * *Kulcs-érték (Key-Value):* Pl. Redis. Gyors, egyszerű.
    * *Dokumentum:* Pl. MongoDB (JSON szerű). Flexibilis séma.
    * *Oszlop-alapú:* Pl. Cassandra. Nagy írási sebesség.
    * *Gráf:* Pl. Neo4j. Kapcsolatok kezelésére.  

## 8. Tétel: Modellezés és SQL
**Téma:** ER/EER modell, Relációs algebra, SQL.

### 8.1 (E)ER Modell
* **Egyed (Entity):** Valós világ objektuma. **Attribútum:** Tulajdonság.
* **Kapcsolat:** Egyedek viszonya. Kardinalitás: 1:1, 1:N, M:N.
* **EER (Kiterjesztett):** Specializáció / Általánosítás (Öröklődés).
* **Leképezés:**
    * 1:N kapcsolat $\to$ Külső kulcs az N oldalon.
    * M:N kapcsolat $\to$ Új kapcsolótábla két külső kulccsal.

### 8.2 Relációs algebra és SQL
* **Relációs algebra (Procedurális):**
    * $\sigma$ (Kiválasztás/Select): Sorok szűrése (`WHERE`).
    * $\pi$ (Vetítés/Project): Oszlopok kiválasztása (`SELECT`).
    * $\bowtie$ (Illesztés/Join): Táblák összekapcsolása (`JOIN`).
* **SQL (Strukturált Lekérdező Nyelv):**
    * *DDL (Definíciós):* `CREATE TABLE`, `ALTER`, `DROP`.
    * *DML (Manipulációs):* `INSERT`, `UPDATE`, `DELETE`, `SELECT`.
    * *DCL (Vezérlő):* `GRANT`, `REVOKE`.  

---

# IV. MESTERSÉGES INTELLIGENCIA

## 9. Tétel: Logikai ágensek
**Téma:** Ágenstípusok, Ítéletkalkulus, Rezolúció.

### 9.1 Ágensek (PEAS modell)
* **PEAS:** Performance (Teljesítmény), Environment (Környezet), Actuators (Beavatkozók), Sensors (Szenzorok).
* **Típusok:**
    1.  *Egyszerű reflex:* Csak az aktuális érzékelésre reagál.
    2.  *Modell alapú:* Van belső állapota a világról (memória).
    3.  *Célalapú:* Tervez, keresést használ a cél eléréséhez.
    4.  *Hasznosság alapú:* A "boldogságot" (hasznosságot) maximalizálja.

### 9.2 Ítéletkalkulus és Bizonyítás
* **Logika:** Szintaktika (jelek) + Szemantika (igazságérték).
* **Következtetés ($KB \models \alpha$):**
    * *Igazságtábla:* Minden lehetséges világ felsorolása (exponenciális).
    * *Rezolúció:* Gépi bizonyítás alapja.
        1.  Állítást tagadjuk ($\neg \alpha$).
        2.  Konjunktív normálformára (CNF) hozzuk (klózok ÉS kapcsolata).
        3.  Rezolúciós lépés: $(A \vee B) \wedge (\neg B \vee C) \to (A \vee C)$.
        4.  Ha kijön az üres klóz $\to$ Ellentmondás $\to$ Az eredeti állítás igaz volt.  

## 10. Tétel: Keresések
**Téma:** Vak és Heurisztikus keresés, Játékok.

### 10.1 Állapottér reprezentáció
Gráf, ahol a csúcsok állapotok, az élek cselekvések.
* **Vak keresések (Nincs infó a cél távolságáról):**
    * *BFS:* Optimális, teljes, de nagy memóriaigény.
    * *DFS:* Nem optimális, nem teljes (végtelen ág), de kis memória.
    * *Iteratívan mélyülő (IDDFS):* A kettő előnyeit ötvözi.

### 10.2 Heurisztikus keresések
* **Heurisztika $h(n)$:** Becslés a célig hátralévő költségről.
* **$A^*$ algoritmus:** $f(n) = g(n) + h(n)$ (eddigi út + becslés). Ha $h(n)$ elfogadható (nem becsül túl), az $A^*$ optimális.
* **Lokális keresések:** Hegymászó (lokális optimumba ragadhat), Szimulált lehűtés (véletlen lépésekkel ugrál ki).

### 10.3 Játékok (Minimax)
* Kétszemélyes, zérus összegű játékok.
* **Minimax elv:** Én maximalizálom a hasznomat, az ellenfél minimalizálja az enyémet.
* **Alfa-Béta vágás:** Ha látok egy lépést, ami biztosan rosszabb, mint amit már találtam máshol, azt az ágat nem fejtem ki tovább.  

## 11. Tétel: Gépi tanulás (ML)
**Téma:** Tanulás típusai, Neurális hálók.

### 11.1 Tanulási paradigmák
* **Felügyelt (Supervised):** Bemenet-kimenet párokból tanul. (Pl. osztályozás, regresszió).
    * *Döntési fa:* Információnyereség (entrópia csökkenés) alapján vág.
* **Nem felügyelt (Unsupervised):** Csak bemenet van, mintázatokat keres. (Pl. Klaszterezés/Csoportosítás - k-means).
* **Megerősítéses (Reinforcement):** Jutalmak/büntetések alapján tanul stratégiát.

### 11.2 Neurális hálózatok (ANN)
* **Neuron modell:** Súlyozott összeg ($w \cdot x + b$) + Aktivációs függvény (pl. Sigmoid, ReLU a nemlinearitáshoz).
* **Tanítás (Backpropagation):**
    1.  Előrecsatolás (kiszámolja a kimenetet).
    2.  Hiba számítása (Loss function).
    3.  Hiba visszaterjesztése: A láncszabály segítségével kiszámolja, hogyan kell módosítani a súlyokat, hogy a hiba csökkenjen (Gradiens ereszkedés).  

---

# V. INFORMATIKAI TÁRGYCSOPORT (Hardver, OS, Hálózat, Szoftver)

## 1. Tétel: Információ reprezentáció
* **Számrendszerek:** Kettes (bináris), Tizenhatos (Hexa). Kettes komplemens (negatív számokhoz).
* **Endianitás:**
    * *Big Endian:* MSB (legnagyobb helyiérték) a legkisebb címen.
    * *Little Endian:* LSB (legkisebb helyiérték) a legkisebb címen (Intel).
* **Lebegőpontos (IEEE 754):** $Szám = (-1)^S \cdot 1.M \cdot 2^{E-bias}$. (Előjel, Mantissza, Kitevő).
* **Hamming kód:** Hibajavító kód (1 bites hiba javítása, 2 bites jelzése) paritásbitekkel.  

## 2. Tétel: ALU (Aritmetikai Logikai Egység)
* **Univerzális teljesség:** NAND vagy NOR kapukkal bármilyen logikai áramkör megépíthető.
* **Összeadók:** Félösszeadó (2 bit), Teljes összeadó (2 bit + carry).
* **Szorzás/Osztás:** Shift (léptetés) és Add/Sub (összeadás/kivonás) műveletek sorozata.  

## 3. Tétel: Vezérlő egység (CU)
* **Feladata:** Utasítások dekódolása, vezérlőjelek kiadása.
* **Huzalozott (Hardwired):** Fizikai kapuk drótozva. Gyors, de nem módosítható. (RISC).
* **Mikrokódos:** A vezérlés egy "belső program" (mikroprogram). Lassabb, de rugalmas, komplex utasításokhoz jó. (CISC).  

## 4. Tétel: Folyamatok (OS)
* **Folyamat (Process):** Futó program példánya. Saját memóriatér.
* **Állapotok:**
    * *Fut (Running):* Övé a CPU.
    * *Kész (Ready):* Vár a CPU-ra.
    * *Blokkolt:* I/O-ra vár.
* **Ütemezés:** Round Robin (időszelet), Prioritásos, FCFS.
* **Szinkronizáció:**
    * *Versenyhelyzet (Race condition):* Több szál írja ugyanazt az adatot $\to$ hiba.
    * *Kritikus szakasz:* A kód veszélyes része.
    * *Szemafor/Mutex:* Eszközök a kölcsönös kizárás megvalósítására.
* **Holtpont (Deadlock):** Mindenki másra vár, a rendszer megáll.  

## 5. Tétel: Tárkezelés
* **Virtuális memória:** A fizikai RAM kiterjesztése a merevlemezre.
* **MMU (Memory Management Unit):** Logikai cím $\to$ Fizikai cím fordítás.
* **Lapozás (Paging):** Fix méretű lapok. Nincs külső töredezettség.
* **Szegmentálás:** Logikai egységek (kód, adat). Van külső töredezettség.
* **Lapcsere stratégiák:** Ha betelik a RAM, mit dobjunk ki?
    * *FIFO:* Legrégebbit (rossz).
    * *LRU:* Legrégebben használtat (jó, de drága).  

## 6. Tétel: Háttértárak
* **RAID (Redundáns Tömb):**
    * *RAID 0:* Csíkozás (gyors, nem biztonságos).
    * *RAID 1:* Tükrözés (biztonságos, drága).
    * *RAID 5:* Paritás (jó kompromisszum).
* **Állományrendszer:**
    * *i-node:* Unix fájlleíró (metaadatok, blokk címek).
    * *FAT:* Láncolt allokáció.
* **RPC (Remote Procedure Call):** Távoli eljáráshívás hálózaton keresztül.  

## 7-9. Tétel: Számítógép-hálózatok
* **Rétegek (OSI/TCP-IP):**
    1.  **Fizikai:** Bitek, kábelek, topológiák.
    2.  **Adatkapcsolati:** Keretek, MAC cím, Switch (ütközési tartományok szétválasztása).
    3.  **Hálózati:** Csomagok, IP cím (v4/v6), Router (útválasztás), NAT (címfordítás), ICMP (ping).
    4.  **Szállítási:**
        * *TCP:* Megbízható, sorszámozott, nyugtázott, kapcsolat-alapú (3-way handshake). Torlódáskezelés.
        * *UDP:* Nem megbízható, gyors (videó, DNS). Portszámok (alkalmazás azonosítása).  

## 10. Tétel: Szoftvertechnológia alapok
* **Vízesés modell:** Lineáris, dokumentált, de merev.
* **Spirális modell:** Kockázat-vezérelt. Ciklikus.
* **Agilis/Iteratív:** Rövid ciklusok (Sprints), folyamatos visszajelzés, változáskövetés. (Pl. Scrum, XP).
* **Specifikáció:** Mit csináljon a rendszer? (Követelmények).  

## 11. Tétel: OOP és UML
* **OOP elvek:** Egységbezárás, Öröklődés, Polimorfizmus.
* **UML Diagramok:**
    * *Use Case:* Felhasználói funkciók.
    * *Class:* Osztályok szerkezete és kapcsolatai (Asszociáció, Aggregáció, Kompozíció).
    * *Sequence:* Időbeli lefolyás, üzenetváltások.
    * *State:* Állapotátmenetek.
* **RUP (Rational Unified Process):** Fázisok: Inception (Előkészítés), Elaboration (Kidolgozás), Construction (Megvalósítás), Transition (Átadás).  

## 12. Tétel: Szoftvertesztelés
* **Validáció:** Megfelelő terméket gyártunk? (Felhasználói igény).
* **Verifikáció:** Helyesen gyártjuk a terméket? (Specifikáció).
* **Módszerek:**
    * *Black-box:* Belső működést nem látjuk (Interfész teszt).
    * *White-box:* Kódszintű teszt (pl. Coverage mérés).
* **V-modell szintek:** Unit teszt (modul) $\to$ Integrációs teszt $\to$ Rendszer teszt $\to$ Átvételi (Acceptance) teszt.  