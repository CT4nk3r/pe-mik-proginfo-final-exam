# PROGRAMTERVEZŐ INFORMATIKUS BSC ZÁRÓVIZSGA KIDOLGOZÁS
**Forrás:** Pannon Egyetem MIK Tematika (2025)

---

# I. SZÁMÍTÁSELMÉLETI TÁRGYCSOPORT

## 1. Tétel: Reguláris nyelvek
>**Kulcsszavak:** Definíció reguláris kifejezéssel, véges automaták (DFA, NFA), ekvivalencia, zártsági tételek.

### 1.1 Alapfogalmak és Halmazelmélet
* **Ábécé ($\Sigma$):** Szimbólumok véges, nem üres halmaza.
* **Szó:** Az ábécé elemeiből képzett véges sorozat. Üres szó: $\varepsilon$.
* **Nyelv ($L$):** Szavak tetszőleges halmaza ($\Sigma^*$ részhalmaza).
* **Skatulya-elv:** Ha $n$ elemet $m$ halmazba osztunk és $n > m$, legalább egy halmazba több elem kerül (pumpálási lemma alapja).

### 1.2 Reguláris kifejezések (RE)
Rekurzív definíció:
1.  $\emptyset, \varepsilon, a \in \Sigma$ reguláris kifejezések.
2.  Ha $R_1, R_2$ regulárisak, akkor $(R_1 \cup R_2)$, $(R_1 \cdot R_2)$, és $R_1^*$ is azok.

### 1.3 Véges automaták
* **DFA (Determinisztikus):** $M = (Q, \Sigma, \delta, q_0, F)$. Minden (állapot, bemenet) párhoz pontosan egy új állapot tartozik.
* **NFA (Nem-determinisztikus):** Egy állapothoz több átmenet is tartozhat, illetve létezhet $\varepsilon$-átmenet.

### 1.4 Ekvivalencia és Átalakítások
* **NFA $\to$ DFA (Hatványhalmaz konstrukció):** Az NFA állapotainak részhalmazai alkotják a DFA állapotait.
* **Reguláris kifejezés $\to$ NFA:** Komponensenként építjük fel (unió, konkatenáció, csillag) $\varepsilon$-átmenetekkel.

### 1.5 Zártsági tételek
A reguláris nyelvek osztálya zárt a következőkre: Unió, Metszet, Komplementer, Konkatenáció, Kleene-csillag, Tükrözés.

---

## 2. Tétel: Környezetfüggetlen nyelvek
>**Kulcsszavak:** CFG, Veremautomata (PDA), ekvivalencia, CFG $\to$ PDA, pumpálási tétel.

### 2.1 Környezetfüggetlen nyelvtan (CFG)
$G = (V, \Sigma, P, S)$. Szabályok alakja: $A \to \gamma$, ahol $A$ nemterminális.
* **Származtatás:** Szabályok alkalmazása a kezdőszimbólumtól a terminális szóig.
* **Egyértelműség:** Egy szónak csak egy levezetési fája létezik.

### 2.2 Veremautomata (PDA)
Véges automata kiegészítve egy veremmel (LIFO).
* **Működés:** $M = (Q, \Sigma, \Gamma, \delta, q_0, Z_0, F)$. Az átmenet függ a bemenettől és a verem tetejétől.
* **N-PDA vs D-PDA:** A nem-determinisztikus PDA erősebb! (A CF nyelveket az N-PDA ismeri fel).

### 2.3 Ekvivalencia (CFG $\to$ PDA)
Minden CFG-hez létezik PDA.
* **Konstrukció:** A PDA a veremben szimulálja a baloldali levezetést. Ha nemterminális van a veremtetőn, szabályt tippel (pop+push). Ha terminális, egyezteti a bemenettel.

### 2.4 Zártsági tételek
* **Zárt:** Unió, Konkatenáció, Kleene-csillag, Tükrözés.
* **NEM zárt:** Metszet, Komplementer.

---

## 3. Tétel: Turing elfogadható nyelvek
>**Kulcsszavak:** Turing gép, Machine Schema, eldönthetőség vs elfogadhatóság, megállási probléma.

### 3.1 Turing-gép (TM)
$M = (Q, \Sigma, \Gamma, \delta, q_0, q_{acc}, q_{rej})$. Végtelen szalag, író-olvasó fej (jobbra/balra mozoghat).
* Ez a modell minden algoritmizálható problémát képes leírni (Church-Turing tézis).

### 3.2 Machine Schema
Elemi gépekből (Jobbra, Balra, Ír) összetett gépek építése: Másoló gép, Shiftelő gép, $a^n b^n c^n$-t felismerő gép.

### 3.3 Nyelvosztályok
* **Eldönthető (Rekurzív):** A TM minden bemenetre megáll (Igen/Nem).
* **Elfogadható (Rekurzívan felsorolható):** Ha $w \in L$, a gép megáll és elfogad. Ha $w \notin L$, a gép vagy elutasít, vagy **végtelen ciklusba** kerül.

### 3.4 Kapcsolat
Minden eldönthető nyelv elfogadható, de fordítva nem igaz.
* **Megállási probléma:** Nem létezik algoritmus, amely eldönti, hogy egy tetszőleges TM megáll-e. (Ez egy elfogadható, de nem eldönthető nyelv).

---

# II. ALGORITMUSOK ÉS ADATSZERKEZETEK

## 4. Tétel: Algoritmusok futási ideje, Rendezések
>**Kulcsszavak:** Aszimptotikus jelölések, rendezések ($O(n^2)$, $O(n \log n)$, lineáris).

### 4.1 Aszimptotikus jelölések
* **$O(n)$ - Ordo:** Felső korlát (legrosszabb eset).
* **$\Omega(n)$ - Omega:** Alsó korlát (legjobb eset).
* **$\Theta(n)$ - Theta:** Pontos korlát.

### 4.2 Rendező algoritmusok
1.  **Négyzetes $O(n^2)$:** Buborék, Beszúró (jó majdnem rendezettnél), Kiválasztó.
2.  **Logaritmikus $O(n \log n)$:**
    * *Merge Sort:* Stabil, oszd-meg-és-uralkodj.
    * *Quick Sort:* Átlagosan nagyon gyors, particionálás vezérelemmel.
    * *Heap Sort:* Helyben rendez, kupac adatszerkezettel.
3.  **Lineáris $O(n)$:** Leszámláló, Edényrendezés (csak speciális bemenetre).

---

## 5. Tétel: Adatszerkezetek
>**Kulcsszavak:** Verem, sor, lista, BST, Kupac, Piros-fekete fa, B-fa, Hash.

### 5.1 Elemi szerkezetek
* **Verem (Stack):** LIFO. Műveletek: push, pop ($O(1)$).
* **Sor (Queue):** FIFO. Műveletek: enqueue, dequeue ($O(1)$).
* **Láncolt lista:** Dinamikus méret, beszúrás $O(1)$, keresés $O(n)$.

### 5.2 Fák
* **Bináris Keresőfa (BST):** Bal gyerek < Szülő $\le$ Jobb gyerek. Keresés átlagosan $O(\log n)$, legrosszabb $O(n)$.
* **Kupac (Heap):** Teljes bináris fa. Max-kupac: szülő $\ge$ gyerekek. Priority Queue alapja.
* **Piros-Fekete fa:** Kiegyensúlyozott BST. Garantálja a $O(\log n)$ magasságot színezéssel és forgatásokkal.
* **B-fa:** Többágú kiegyensúlyozott fa, lemezes tároláshoz optimalizálva (adatbázis indexek).

### 5.3 Hasító táblázatok (Hash)
Kulcs $\to$ Index leképezés.
* **Ütközéskezelés:** Láncolás (lista az indexen) vagy Nyílt címzés (új hely keresése).

---

## 6. Tétel: Gráf algoritmusok
>**Kulcsszavak:** BFS, DFS, MST (Prim, Kruskal), Legrövidebb út (Dijkstra, Bellman-Ford), Max folyam.

### 6.1 Bejárások
* **Szélességi (BFS):** Sorral. Legrövidebb utat ad súlyozatlan gráfban.
* **Mélységi (DFS):** Veremmel/Rekurzióval. Topologikus rendezéshez.

### 6.2 Minimális Feszítőfák (MST)
* **Kruskal:** Élek rendezése súly szerint, unió, ha nincs kör.
* **Prim:** Kezdőcsúcsból növeszti a fát a legkisebb elérhető éllel.

### 6.3 Legrövidebb utak
* **Dijkstra:** Nemnegatív élsúlyokra. Mohó (Priority Queue).
* **Bellman-Ford:** Negatív élekre is jó. Detektálja a negatív köröket.

### 6.4 Maximális folyam
* **Ford-Fulkerson:** Javítóutak keresése a maradék hálózatban. Max-Flow Min-Cut tétel.

---

# III. ADATBÁZIS-KEZELÉS

## 7. Tétel: Relációs elmélet és NoSQL
>**Kulcsszavak:** Redundancia, Anomáliák, Normalizálás, NoSQL, CAP.

### 7.1 Relációs modell hibái
* **Redundancia:** Felesleges adatduplikáció.
* **Anomáliák:** Beszúrási, Törlési, Módosítási (inkonzisztencia veszélye).

### 7.2 Normalizálás
* **1NF:** Elemi értékek.
* **2NF:** Nincs részleges függőség (összetett kulcs esetén).
* **3NF:** Nincs tranzitív függőség (nem-kulcs nem függ nem-kulcstól).
* **BCNF:** Minden determináns jelölt kulcs.

### 7.3 NoSQL
* **CAP tétel:** Konzisztencia, Rendelkezésre állás, Partíciótűrés – egyszerre csak kettő lehetséges.
* **Típusok:** Key-Value (Redis), Document (MongoDB), Columnar, Graph.

---

## 8. Tétel: Tervezés és SQL
>**Kulcsszavak:** ER modell, EER, Relációs algebra, SQL utasítások.

### 8.1 Modellezés
* **ER:** Egyedek, Attribútumok, Kapcsolatok (1:1, 1:N, M:N).
* **EER:** Öröklődés (Specializáció/Generalizáció).
* **Leképezés:** M:N kapcsolat $\to$ Kapcsolótábla.

### 8.2 Lekérdezések
* **Relációs Algebra:** Procedurális ($\sigma$ kiválasztás, $\pi$ vetítés, $\bowtie$ join).
* **SQL:** Deklaratív (`SELECT`... `FROM`... `WHERE`).
    * DDL: `CREATE`, `DROP`.
    * DML: `INSERT`, `UPDATE`, `DELETE`.

---

# IV. MESTERSÉGES INTELLIGENCIA

## 9. Tétel: Ágensek és Logika
>**Kulcsszavak:** Ágenstípusok, PEAS, Ítéletkalkulus, Rezolúció.

### 9.1 Ágensek
Szenzor $\to$ [Ágens] $\to$ Beavatkozó.
* **Típusok:** Reflex, Modell alapú, Célalapú, Hasznosság alapú.
* **Környezet:** Megfigyelhető?, Determinisztikus?, Statikus?

### 9.2 Logika
* **Ítéletkalkulus:** Igaz/Hamis állítások, logikai műveletek.
* **Bizonyítás:** Igazságtábla (lassú), Rezolúció (CNF alak, ellentmondásos bizonyítás üres klózzal).

## 10. Tétel: Keresések
>**Kulcsszavak:** Állapottér, Vak keresés, Heurisztika ($A^*$), Minimax.

### 10.1 Keresési típusok
* **Vak:** BFS (optimális), DFS (kis memória), IDDFS.
* **Heurisztikus:** $f(n) = g(n) + h(n)$.
    * **$A^*$:** Ha $h(n)$ elfogadható (nem becsül túl), optimális utat talál.
* **Lokális:** Hegymászó módszer, Szimulált lehűtés.

### 10.2 Játékok
* **Minimax:** Kétszemélyes, zérus összegű játékok. (MAX vs MIN).
* **Alfa-Béta vágás:** A fa felesleges ágainak levágása a keresés gyorsítására.

## 11. Tétel: Gépi tanulás
>**Kulcsszavak:** Felügyelt/Nem felügyelt, Neurális hálók, Backpropagation.

### 11.1 Tanulási típusok
* **Felügyelt:** Címkézett adatok (Osztályozás, Regresszió).
* **Nem felügyelt:** Nincs címke (Klaszterezés, pl. k-means).
* **Megerősítéses:** Jutalom/Büntetés alapú.

### 11.2 Neurális hálók
* **Neuron:** Súlyozott összeg + Aktivációs függvény (Sigmoid, ReLU).
* **Tanítás:** Hiba-visszaterjesztés (Backpropagation) $\to$ Súlyok módosítása gradiens ereszkedéssel.
* **Mélytanulás:** Sok rejtett réteg, automatikus feature extraction.

---

# V. INFORMATIKAI TÁRGYCSOPORT (Hardver, OS, Hálózat)

## 1. Információ reprezentáció
* **Számrendszerek:** 2-es, 16-os.
* **Endianitás:** Big vs Little Endian.
* >**Lebegőpontos:** IEEE 754 (Előjel, Kitevő, Mantissza).

## 2. ALU
* **Logika:** Univerzális teljesség (NAND kapuk).
* **Aritmetika:** Félösszeadó, Teljes összeadó. >Kivonás kettes komplemenssel.

## 3. Vezérlő egység (CU)
* **Huzalozott:** Gyors, fix logikai kapuk (RISC).
* >**Mikrokódos:** Rugalmas, belső memóriából olvassa a vezérlést (CISC).

## 4. Folyamatok (OS)
* **Állapotok:** Fut, Kész, Blokkolt. Környezetváltás.
* **Szinkronizáció:** Kritikus szakasz védelme (Szemafor, Mutex) a versenyhelyzet ellen.
* >**Holtpont:** Cirkuláris várás erőforrásokra.

## 5. Tárkezelés
* **Virtuális memória:** MMU fordítja a címeket.
* **Lapozás:** Fix méretű blokkok. >Lapcsere: LRU (legrégebben használt).

## 6. Háttértárak
* **RAID:** 0 (gyors), 1 (tükör), 5 (paritás).
* >**Fájlrendszer:** Allokációs táblák, i-node.

## 7-9. Hálózatok (OSI alsó rétegek)
* **Fizikai/Adatkapcsolati:** MAC cím, Switch, Keretezés.
* **Hálózati:** IP címzés (v4/v6), Routing, NAT.
* >**Szállítási:** TCP (megbízható, 3-utas kézfogás), UDP (gyors, streaming).

---

# VI. SZOFTVERTECHNOLÓGIA

## 10. Szoftvergyártás
* **Modellek:** Vízesés (szekvenciális), Spirális (kockázat alapú), Agilis/Iteratív.
* >**Lépések:** Specifikáció $\to$ Tervezés $\to$ Implementáció $\to$ Validáció.

## 11. OOP és UML
* **UML Diagramok:**
    * *Use Case:* Funkciók, aktorok.
    * *Class:* Statikus szerkezet.
    * *Sequence:* Időbeli üzenetváltás.
    * *State:* Állapotátmenetek.
* >**RUP:** Modern, iteratív keretrendszer (Inception, Elaboration, Construction, Transition).

## 12. Tesztelés
* **Módszerek:** Black-box (bemenet/kimenet), White-box (belső kód).
* **Szintek:** Unit $\to$ Integrációs $\to$ Rendszer $\to$ Átvételi.
* >**Validáció vs Verifikáció:** Jót csinálunk? vs Jól csináljuk?.