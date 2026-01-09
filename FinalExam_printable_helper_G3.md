# Programtervező Informatikus BSc Záróvizsga Kidolgozott Tételek
*Forrás: 250320-PI-BSc-zarovizsga-tematika-250320.pdf  *

---

## I. SZÁMÍTÁSELMÉLETI TÁRGYCSOPORT  

### 1. Reguláris nyelvek  
**Kulcsfogalmak:** Reguláris kifejezések, DFA, NFA, ekvivalencia, zártsági tételek.

#### 1.1 Alapfogalmak  
* **Ábécé ($\Sigma$):** Szimbólumok véges, nem üres halmaza.
* **Szó:** Az ábécé elemeiből képzett véges sorozat. Üres szó: $\varepsilon$.
* **Nyelv ($L$):** Szavak egy részhalmaza ($\Sigma^*$-on).
* **Műveletek nyelvekkel:** Unió, konkatenáció, Kleene-csillag (iteráció), metszet, komplementer.

#### 1.2 Reguláris nyelvek definíciója  
Egy nyelv reguláris, ha leírható reguláris kifejezéssel.
**Reguláris kifejezések (RK) felépítése:**
1.  $\emptyset, \varepsilon$ és $a$ (ahol $a \in \Sigma$) reguláris kifejezések.
2.  Ha $R$ és $S$ RK, akkor $(R+S)$, $(RS)$, és $R^*$ is azok.

#### 1.3 Véges automaták  
A reguláris nyelveket felismerő gépek.
* **DFA (Determinisztikus Véges Automata):** $M = (Q, \Sigma, \delta, q_0, F)$
    * $Q$: Állapotok véges halmaza.
    * $\delta$: Átmenetfüggvény ($Q \times \Sigma \to Q$). Minden állapothoz és bemenethez pontosan egy új állapot tartozik.
    * $q_0$: Kezdőállapot.
    * $F$: Elfogadó állapotok halmaza.
* **NFA (Nemdeterminisztikus Véges Automata):**
    * Az átmenetfüggvény: $Q \times (\Sigma \cup \{\varepsilon\}) \to P(Q)$.
    * Egy állapothoz több következő állapot is tartozhat, vagy $\varepsilon$-lépés is lehetséges.

#### 1.4 Ekvivalencia és Átalakítások  
**Tétel:** A DFA, NFA és a Reguláris Kifejezések kifejezőereje megegyezik.
1.  **NFA $\to$ DFA (Részhalmaz-konstrukció):**
    * A DFA állapotai az NFA állapotainak részhalmazai lesznek.
    * Ha az NFA-nak $n$ állapota van, a DFA-nak legfeljebb $2^n$.
    * Kezdőállapot: az NFA kezdőállapotának $\varepsilon$-lezártja.
2.  **Reguláris kifejezés $\to$ NFA (Thompson-konstrukció):**
    * Elemi automaták építése ($\varepsilon$, $a$).
    * Kompozíció: Unió (párhuzamos elágazás), Konkatenáció (sorbakötés), Csillag (visszacsatolás $\varepsilon$-val).

#### 1.5 Zártsági tételek és szivattyúzó (pumpáló) lemma  
* **Zártság:** A reguláris nyelvek zártak az unióra, metszetre, komplementerre, konkatenációra és csillagra.
* **Pumping lemma (Skatulya elv):** Ha $L$ reguláris, akkor van olyan $p$ pumpálási hossz, hogy minden $w \in L, |w| \ge p$ felbontható $w=xyz$ alakra úgy, hogy:
    1.  $xy^iz \in L$ minden $i \ge 0$-ra.
    2.  $|y| > 0$.
    3.  $|xy| \le p$.
    * *Alkalmazás:* Annak bizonyítása, hogy egy nyelv NEM reguláris (pl. $a^n b^n$).

---

### 2. Környezetfüggetlen nyelvek (CFL)  
**Kulcsfogalmak:** CFG, PDA, származtatás, Chomsky-normálforma, pumpáló lemma.

#### 2.1 Környezetfüggetlen nyelvtan (CFG)  
Definíció: $G = (V, \Sigma, R, S)$
* $V$: Nemterminálisok halmaza.
* $\Sigma$: Terminálisok (ábécé).
* $R$: Szabályok ($A \to \beta$, ahol $A \in V, \beta \in (V \cup \Sigma)^*$).
* $S$: Kezdőszimbólum.
* **Származtatás:** A kezdőszimbólumból indulva szabályok alkalmazása, amíg csak terminálisok maradnak.

#### 2.2 Veremautomaták (PDA)  
Olyan véges automata, amely rendelkezik egy **veremmel** (LIFO memória).
* A verem lehetővé teszi pl. zárójelek párosításának ellenőrzését.
* **Definíció:** $M = (Q, \Sigma, \Gamma, \delta, q_0, Z_0, F)$. ($\Gamma$ a veremábécé).
* A PDA lehet determinisztikus (DPDA) és nemdeterminisztikus. **A CFL osztályt a nemdeterminisztikus PDA-k fedik le.**

#### 2.3 Ekvivalencia és Zártság  
* **CFG $\to$ PDA:** Olyan PDA építése, ami szimulálja a baloldali levezetést a veremben.
* **Zártsági tételek:**
    * Zárt: Unió, Konkatenáció, Kleene-csillag.
    * **NEM zárt:** Metszet, Komplementer. (Példa: $a^n b^n c^n$ nem CFL, de előállhat két CFL metszeteként).

#### 2.4 Második Pumpáló Lemma
Hasonló a regulárishoz, de itt a szót 5 részre bontjuk: $w = uvxyz$.
* $uv^ixy^iz \in L$ minden $i$-re.
* $|vy| > 0$ és $|vxy| \le p$.

---

### 3. Turing elfogadható nyelvek  
**Kulcsfogalmak:** Turing-gép, Church-Turing tézis, Megállási probléma, R és RE nyelvek.

#### 3.1 Turing-gép (TM) definíciója  
A legáltalánosabb számítási modell.
* Végtelen szalag, író-olvasó fej, véges vezérlő.
* Lépés: (jelenlegi állapot, olvasott jel) $\to$ (új állapot, írt jel, fejmozgás L/R).
* **Church-Turing tézis:** Minden, ami algoritmikusan kiszámítható, az kiszámítható Turing-géppel is.

#### 3.2 Nyelvosztályok  
* **Turing-elfogadható (Rekurzívan felsorolható, RE):** Van olyan TM, amely minden $w \in L$ szóra megáll és elfogad, de $w \notin L$ esetén lehet, hogy végtelen ciklusba kerül.
* **Turing-eldönthető (Rekurzív, R):** Van olyan TM, amely minden bemenetre megáll (igen/nem választ ad).
* **Kapcsolat:** $R \subset RE$. (Minden eldönthető nyelv elfogadható, de fordítva nem).

#### 3.3 Eldönthetetlenség
* **Megállási probléma:** Nem létezik olyan algoritmus, amely tetszőleges TM-ről és bemenetről eldönti, hogy a gép megáll-e.
* **Diagonalizációs elv:** Ezzel bizonyítható, hogy a valós számok nem megszámlálhatók, és emiatt léteznek nem Turing-felismerhető nyelvek.

---

### 4. Algoritmusok futási ideje, Rendező és Kereső algoritmusok  

#### 4.1 Aszimptotikus jelölések  
* **$O(g(n))$:** Felső korlát (legrosszabb eset).
* **$\Omega(g(n))$:** Alsó korlát.
* **$\Theta(g(n))$:** Pontos nagyságrend (aszimptotikusan szoros korlát).

#### 4.2 Rendező algoritmusok  
* **Négyzetes $O(n^2)$:**
    * *Buborék (Bubble):* Szomszédos elemek cseréje.
    * *Beszúró (Insertion):* Kártyarendezés elv, kis listákra jó.
    * *Kiválasztó (Selection):* Minimum keresése és elejére cserélése.
* **Logaritmikus $O(n \log n)$:**
    * *Összefésülő (Merge):* Oszd meg és uralkodj. Stabil, de extra memóriát igényel.
    * *Gyorsrendezés (Quick):* Pivot választás, particionálás. Átlag $n \log n$, de legrosszabb $n^2$. Helyben rendez.
    * *Kupacrendezés (Heap):* Kupac adatszerkezet építése (max-heap), gyökér cseréje az utolsóval. Garantált $n \log n$, nem stabil.
* **Lineáris $O(n)$** (speciális feltételekkel):
    * *Leszámláló (Counting):* Ha az elemek kis intervallumból valók.
    * *Edény (Bucket) és Számjegyes (Radix).*

#### 4.3 Kereső algoritmusok  
* **Lineáris keresés:** $O(n)$, rendezetlen tömbön.
* **Bináris keresés:** $O(\log n)$, rendezett tömbön (felezéses módszer).

---

### 5. Elemi és fejlett adatszerkezetek  

#### 5.1 Elemi szerkezetek  
* **Verem (Stack):** LIFO. Műveletek: push, pop ($O(1)$).
* **Sor (Queue):** FIFO. Műveletek: enqueue, dequeue ($O(1)$).
* **Láncolt listák:**
    * *Egyszeresen:* Csak előre mutató pointer.
    * *Kétszeresen:* Előre és hátra mutató pointerek (törlés könnyebb).
    * Előny: Dinamikus méret. Hátrány: Szekvenciális elérés $O(n)$.

#### 5.2 Fák és Keresőfák  
* **Bináris Keresőfa (BST):** Bal gyerek < Szülő < Jobb gyerek.
    * Keresés/Beszúrás: Átlag $O(\log n)$, legrosszabb (elfajult fa) $O(n)$.
* **Piros-fekete fák:** Kiegyensúlyozott BST.
    * Tulajdonságok: Gyökér fekete, pirosnak nem lehet piros gyereke, minden úton ugyanannyi fekete csúcs.
    * Garantálja a $O(\log n)$ műveletigényt (forgatásokkal).
* **B-fák:** Többutas keresőfák, adatbázisokhoz/fájlrendszerekhez optimalizálva (lemezkezelés minimalizálása). Minden csúcsban több kulcs van.

#### 5.3 Hasító táblázatok (Hash Tables)  
* **Elv:** Kulcs leképzése indexre egy $h(k)$ függvénnyel.
* **Ütközéskezelés:**
    1.  *Láncolás:* A tábla minden cellája egy listafej.
    2.  *Nyílt címzés:* Ha foglalt a hely, keresünk másikat (pl. lineáris próba).
* **Futási idő:** Átlag $O(1)$, legrosszabb $O(n)$.

---

### 6. Gráf algoritmusok  
**Reprezentáció:** Szomszédsági mátrix (sűrű gráfokhoz), Szomszédsági lista (ritka gráfokhoz) .

#### 6.1 Bejárások
* **Szélességi (BFS):** Sor adatszerkezet. Legrövidebb út élek számában. $O(V+E)$.
* **Mélységi (DFS):** Verem (vagy rekurzió). Topológiai rendezéshez, komponensek kereséséhez. $O(V+E)$.

#### 6.2 Minimális feszítőfák (MST)  
* **Kruskal:** Élek súly szerinti rendezése, legkisebb hozzáadása, ha nem okoz kört (Unió-Holvan adatszerkezettel).
* **Prim:** Egy csúcsból indulva mindig a legközelebbi elérhető csúcs hozzáadása (Priority Queue-val).

#### 6.3 Legrövidebb utak  
* **Dijkstra:** Nemnegatív élsúlyok esetén. Mohó algoritmus. $O(E + V \log V)$ (Fibonacci kupaccal).
* **Bellman-Ford:** Negatív élek esetén is működik (negatív kört detektál). $O(V \cdot E)$.

#### 6.4 Maximális folyam  
* **Ford-Fulkerson:** Javítóutak keresése a maradék hálózatban, amíg van.
* **Vágás tétel:** Max folyam értéke = Min vágás kapacitása.

---

### 7. Relációs adatbázisok - Normalizálás  

#### 7.1 Redundancia és anomáliák  
* **Beszúrási anomália:** Nem tudunk adatot felvinni, mert hiányzik a kulcs egy része.
* **Törlési anomália:** Adat törlésekor elveszhet más, független információ is.
* **Módosítási anomália:** Redundáns adatot több helyen kell javítani.

#### 7.2 Normálformák  
* **1NF:** Minden attribútum atomi (nem osztható), nincs ismétlődő csoport.
* **2NF:** 1NF + minden nem kulcs attribútum teljesen függ az elsődleges kulcstól (nem csak egy részétől összetett kulcs esetén).
* **3NF:** 2NF + nincs tranzitív függőség (nem kulcs nem függ másik nem kulcstól).
* **BCNF:** Szigorúbb 3NF. Minden determináns jelölt kulcs.

#### 7.3 NoSQL rendszerek  
* **CAP tétel:** Konzisztencia (C), Rendelkezésre állás (A), Partíciótűrés (P) - egyszerre csak kettő teljesülhet.
* **Típusok:** Kulcs-érték (Redis), Dokumentum (MongoDB), Oszlop-alapú (Cassandra), Gráf (Neo4j).
* **ACID (RDBMS)** vs **BASE (NoSQL)** elvek.

---

### 8. Koncepcionális adatbázistervezés  

#### 8.1 Modellezés
* **ER modell:** Egyedek (Entity), Kapcsolatok (Relationship), Tulajdonságok.
* **Kardinalitás:** 1:1, 1:N, M:N kapcsolatok.
* **EER:** Öröklődés (IS-A kapcsolat), specializáció/általánosítás .

#### 8.2 Relációs algebra és SQL  
* **Relációs algebra műveletek:**
    * *Szelekció ($\sigma$):* Sorok szűrése (WHERE).
    * *Projekció ($\pi$):* Oszlopok kiválasztása (SELECT).
    * *Descartes-szorzat ($\times$):* Minden párosítás.
    * *Illesztés (Join, $\bowtie$):* Összekapcsolás feltétel alapján.
* **SQL utasítások:**
    * DDL (CREATE, DROP), DML (INSERT, UPDATE, DELETE), DQL (SELECT).

---

### 9. Mesterséges Intelligencia - Logika  

#### 9.1 Ágensek
* **Definíció:** Szenzorokkal érzékel, beavatkozókkal cselekszik.
* **PEAS:** Performance (Teljesítmény), Environment (Környezet), Actuators (Beavatkozók), Sensors (Szenzorok).
* **Típusok:** Reflex ágens, Célalapú, Haszonalapú.

#### 9.2 Ítéletkalkulus  
* **Szintaktika:** Változók, logikai kötőszavak ($\neg, \wedge, \vee, \Rightarrow, \Leftrightarrow$).
* **Szemantika:** Igazságtáblák.
* **Következtetés:**
    * *Modus Ponens:* Ha $A$ és $A \Rightarrow B$, akkor $B$.
    * *Rezolúció:* Gépi bizonyítás alapja. CNF (Konjunktív Normálforma) alakra hozás után ellentmondásos klózok keresése.

---

### 10. Keresési algoritmusok és Játékok  

#### 10.1 Vak keresések  
Nincs információ a céltól való távolságról.
* **Szélességi, Mélységi** (lásd Gráfok).
* **Iteratívan mélyülő:** Mélységi keresés növekvő mélységhatárral (optimális és teljes).

#### 10.2 Heurisztikus keresések  
$f(n) = g(n) + h(n)$, ahol $g$ az útköltség, $h$ a becslés a célig.
* **Mohó keresés:** Csak $h(n)$-t minimalizál. Gyors, de nem optimális.
* **A* algoritmus:** $f(n)$-t minimalizál. Ha $h(n)$ elfogadható (sosem becsüli túl a költséget), akkor az A* optimális és teljes.

#### 10.3 Kétszemélyes játékok  
* **Minimax:** A maximáló játékos a saját hasznát növeli, a minimáló csökkenti. Teljes játékfát épít (elvben).
* **Alfa-béta vágás:** A fa egyes ágainak levágása, ha már találtunk egy jobb lépést máshol (nem kell mindent kiértékelni).

---

### 11. Gépi tanulás  

#### 11.1 Tanulás fajtái  
* **Felügyelt (Supervised):** Címkézett adatok (bemenet-kimenet párok). Pl. osztályozás, regresszió.
* **Felügyelet nélküli (Unsupervised):** Nincs címke, struktúrát keres. Pl. klaszterezés (k-means).
* **Megerősítéses (Reinforcement):** Jutalmak/büntetések alapján tanul (ágens).

#### 11.2 Neurális hálók  
* **Neuron modell:** Bemenetek súlyozott összege + bias $\to$ Aktivációs függvény (Sigmoid, ReLU) $\to$ Kimenet.
* **Tanítás:** Backpropagation (Hiba-visszaterjesztés) algoritmus. Gradiens ereszkedéssel minimalizáljuk a veszteségfüggvényt.
* **Túltanulás (Overfitting):** A modell "bemagolja" a tréning adatokat, de rosszul generalizál. Megoldás: Regularizáció, Drop-out.

---

## II. INFORMATIKAI TÁRGYCSOPORT  

### 1. Információ reprezentáció  
* **Számrendszerek:** Bináris, Hexadecimális. Konverziók.
* **Előjeles számábrázolás:** Kettes komplemens (negatív szám: invertálás + 1). Így a kivonás visszavezethető összeadásra.
* **Lebegőpontos:** IEEE 754 szabvány (Előjel, Karakterisztika/Kitevő, Mantissza). $N = (-1)^S \cdot 1.M \cdot 2^{K-bias}$.

### 2. ALU (Arithmetic Logic Unit)  
* A CPU azon része, amely a számításokat végzi.
* **Felépítés:** Logikai kapukból (AND, OR, NOT, XOR).
* **Összeadók:** Félösszeadó (2 bit), Teljes összeadó (2 bit + carry), Ripple Carry Adder (lassú), Carry Lookahead Adder (gyors).

### 3. Vezérlő egységek (CU)  
* Feladata az utasítások dekódolása és vezérlőjelek kiadása az adatútnak.
* **Huzalozott:** Logikai kapukkal fixen épített (gyors, de nem rugalmas). RISC processzorokban gyakori.
* **Mikrokódos:** A vezérlőjeleket egy belső memóriából (mikroprogram) olvassa ki. Könnyen módosítható, bővíthető utasításkészlet (CISC).

### 4. Operációs Rendszerek - Folyamatok  
* **Folyamat (Process):** Futó program példány. Állapotai: Fut, Kész, Várakozik.
* **Ütemezés:**
    * *Preemptív:* Az OS elveheti a vezérlést (pl. Round Robin).
    * *Nem preemptív:* A folyamat önként adja át (pl. FCFS).
* **Holtpont (Deadlock):** Folyamatok egymásra várnak. Feltételei: Kölcsönös kizárás, Fogva tart és vár, Nincs megszakítás, Ciklikus várakozás.
* **Szinkronizáció:** Szemaforok, Mutexek használata a versenyhelyzetek (Race Condition) elkerülésére a kritikus szakaszoknál .

### 5. Memóriakezelés  
* **Virtuális memória:** A fizikai memóriánál nagyobb címtér illúziója.
* **Lapozás (Paging):** A memóriát fix méretű lapokra osztjuk. Logikai cím $\to$ Fizikai cím fordítás az MMU és laptábla segítségével.
* **Lapcsere stratégiák:** Ha a RAM betelt, kit kell kirakni a lemezre (swap)?
    * *LRU (Least Recently Used):* A régen használtat dobjuk ki.
    * *FIFO:* A legrégebben bent lévőt.

### 6. Háttértárak és Fájlrendszerek  
* **RAID:** Redundáns lemeztömbök.
    * *RAID 0:* Csíkozás (gyors, nincs védelem).
    * *RAID 1:* Tükrözés (biztonságos, tárhely fele).
    * *RAID 5:* Paritás (gyors olvasás, 1 lemez kiesést bír).
* **Fájlrendszer:** Könyvtárszerkezet, i-node-ok (Linux), FAT/NTFS (Windows). Jogosultságkezelés.

### 7. Hálózatok - Fizikai és Adatkapcsolati réteg  
* **OSI Modell alsó rétegei.**
* **Fizikai:** Kábelek (UTP, Optika), jelek átvitele (feszültség, fény).
* **Adatkapcsolati:**
    * *Keretezés:* Bitekből keretek.
    * *MAC cím:* Fizikai címzés (48 bit hex).
    * *Switch:* MAC cím alapján továbbít, nem szór (mint a Hub).
    * *CSMA/CD:* Ütközésérzékelés (Ethernet).

### 8. Hálózatok - Hálózati réteg  
* **Feladat:** Csomagok továbbítása hálózatok között (Routing).
* **IP címzés:**
    * *IPv4:* 32 bit (pl. 192.168.0.1). Osztályos vs CIDR (netmask).
    * *IPv6:* 128 bit, kimeríthetetlen.
* **Router:** Útválasztó eszköz. Protokollok: OSPF (belső), BGP (külső).
* **NAT:** Privát címek fordítása publikusra.

### 9. Hálózatok - Szállítási réteg  
* **Feladat:** Végpontok közötti kommunikáció. Portszámok.
* **TCP (Transmission Control Protocol):** Megbízható, összeköttetés-alapú.
    * Handshake: SYN, SYN-ACK, ACK.
    * Ablakmechanizmus (Flow control), torlódáskezelés.
* **UDP (User Datagram Protocol):** Nem megbízható, gyors, összeköttetés-mentes (pl. streaming, DNS).

### 10. Szoftvertechnológia alapok  
* **Vízesés modell:** Lineáris (Specifikáció $\to$ Tervezés $\to$ Imp. $\to$ Teszt). Nehéz visszalépni.
* **Iteratív/Inkrementális:** A rendszer darabokban készül el.
* **Agilis:** Változásra reagálás (Scrum, XP). Rövid sprintek, folyamatos visszajelzés.
* **Szoftver életciklus:** Követelményelemzés, Tervezés, Implementáció, Tesztelés, Karbantartás.

### 11. OO Tervezés és UML  
* **OOP elvek:** Egységbezárás, Öröklődés, Polimorfizmus.
* **UML Diagramok:**
    * *Use Case:* Felhasználói funkciók.
    * *Class:* Osztályok szerkezete és kapcsolatai.
    * *Sequence:* Objektumok időbeli kommunikációja.
    * *State:* Állapotátmenetek.
* **RUP (Rational Unified Process):** Fázisok (Inception, Elaboration, Construction, Transition).

### 12. Szoftvertesztelés  
* **V&V:** Verifikáció (Jól csináljuk a terméket?) vs Validáció (A jó terméket csináljuk? - megfelel az igényeknek).
* **Módszerek:**
    * *Fehér doboz:* Ismerjük a forráskódot (pl. ág-lefedettség mérése).
    * *Fekete doboz:* Csak a bemenet/kimenet ismert (pl. ekvivalencia-partícionálás).
* **Szintek:** Egységteszt (Unit), Integrációs teszt, Rendszerteszt, Átvételi teszt.