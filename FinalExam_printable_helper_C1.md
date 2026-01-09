# Bevezetés
Ez a dokumentum a csatolt tételsor minden tételét részletezi: definíciók, kulcsfogalmak, fontos állítások/bizonyítások vázlatai, algoritmusok lépései, komplexitások, tipikus vizsgakérdések és mintafeladatok megoldási irányai. A cél: hogy a tételsor alapján sikeresen fel tudj készülni a záróvizsgára.

# 1. Reguláris nyelvek
**Definíció:** reguláris kifejezéssel leírható nyelvek; véges automatákkal (DFA/NFA) felismerhető nyelvek.  
**Kulcsfogalmak:** ábécé, szavak, nyelvek, DFA, NFA, ε-átmenetek, reguláris kifejezések (union, konkatenáció, Kleene-csillag).  
**Ekvivalencia és konstrukciók:**  
- NFA → DFA (subset construction): állapotok halmazainak kezelése, komplexitás worst-case \(2^n\).  
- Reguláris kifejezés → NFA: Thompson-konstrukció (ε-átmenetekkel), egyszerű és rendszerezett.  
**Zártsági tételek:** unió, konkatenáció, Kleene-csillag, metszet, komplementer, különbség (komplementerhez DFA és teljesítés szükséges).  
**Fontos tételek/bizonyítások:** Pumping lemma reguláris nyelvekre (kizáró bizonyításokhoz).  
**Példák:** L = {a^n b^m | n,m ≥ 0} reguláris; L = {a^n b^n | n≥0} nem reguláris.  
**Gyakori vizsgakérdés:** NFA → DFA lépéseinek bemutatása konkrét példán; pumping lemma alkalmazása nem-reguláris nyelv igazolására.

# 2. Környezetfüggetlen nyelvek (CFG, PDA)
**Definíció:** CFG (V, Σ, R, S) — bal/közép/jobbszármaztatás, derivációk.  
**Felismerés:** pushdown automaton (PDA) — egy verem, determinisztikus vs. nem-determinisztikus.  
**Ekvivalencia:** minden CFG-hez van PDA (kosárcsapdás konstrukciók: könyv szerint a szabványos eljárások).  
**Pumpálási tétel (CFL):** második pumpálási tétel specifikus formája; használata: bizonyítás, hogy egy nyelv nem kontextusfüggetlen.  
**Zártsági tulajdonságok:** unió, konkatenáció, Kleene-csillag zárt; metszet nem zárt (kivéve reguláris metszettel), komplementer nem zárt általánosan.  
**Példa:** L = {a^n b^n | n≥0} környezetfüggetlen; L = {a^n b^n c^n | n≥0} nem környezetfüggetlen.  
**Gyakorlat:** CFG írata, egyszerű PDA tervezése, derivációs fa rajzolása.

# 3. Turing-elfogadható nyelvek
**Definíció:** Turing-gép (TM): végtelen szalag, fej, állapotok, átmeneti függvény.  
**Fogalmak:** megállás/végállapot, partial vs. total computable funkciók, karakterisztikus függvény.  
**Machine schema:** egyszerű szerkezeti sémák (másoló gép, shift művelet).  
**Turing-elfogadható (recursively enumerable) vs. eldönthető (decidable):**  
- Eldönthető: TM mindig megáll és eldönt.  
- Elfogadható: ha w∈L akkor TM megáll és elfogad; ha w∉L akkor lehet, hogy nem áll meg.  
**Megállási probléma (Halting Problem):** be nem dönthető (Church–Turing tézis; bizonyítás redukcióval).  
**Gyakori feladatok:** TM leírása egyszerű feladatokra, egy nyelv eldönthetőségének/elfogadhatóságának értékelése.

# 4. Algoritmus futási ideje (aszimptotika) és rendezések/keresések
**Aszimptotikus jelölések:** O, Ω, Θ; legjobb/átlagos/legrosszabb eset.  
**Rendezések áttekintése:**  
- Nlogn: Quicksort (átlag), Heapsort (Θ(n log n) worst), Mergesort (Θ(n log n) worst).  
- Quadratic: Bubble, Insertion, Selection (Θ(n^2) worst).  
- Lineáris speciális: Counting, Radix, Bucket (feltételek: korlátozott értékkészlet).  
**Keresések:** Linear search Θ(n); Binary search Θ(log n) (feltétel: rendezett tömb).  
**Elemző gyakorlat:** Adott algoritmus futásidejének számítása, rekurzív relációk megoldása (Master theorem alkalmazása).

# 5. Elemi és fejlett adatszerkezetek
**Alapok:** verem, sor — műveletek, amortizált elemzés.  
**Láncolt listák:** egyszeres, kétszeres, körkörös; beszúrás/törlés O(1) ha adott hivatkozás.  
**Bináris keresőfa (BST):** beszúrás/keresés/törlés átlag O(log n), worst O(n).  
**Kupacok (heaps):** bináris kupac; heapify, extract-min/max és insert műveletek O(log n); heap-sort alkalmazása.  
**Önkiegyenlítő fák:** red-black fa — tulajdonságok, fekete-magasság; beszúrás/törlés algoritmusok rotációkkal O(log n).  
**B-fák:** definíció, magasság becslése, lapokban kulcsok, disk-orientált műveletek.  
**Hasító táblák (hash tables):** ütközéskezelés: láncolás, nyílt címzés (linear/quadratic probing), dupla hash; amortizált O(1) műveletek.  
**Gyakorlati feladat:** red-black fa beszúrási lépéseinek bemutatása, hash-függvény kiválasztásának elvei.

# 6. Gráf algoritmusok
**Ábrázolás:** szomszédsági lista vs. mátrix; tárolási költségek.  
**Keresések:** DFS (mélységi), BFS (szélességi) — idő O(V+E).  
**Minimális feszítőfák:** Prim (heap alapú implementáció O(E log V)), Kruskal (egyesítés-find struktúrával O(E log E)).  
**Legrövidebb utak:** Dijkstra (nem-negatív élsúlyok, O(E + V log V) heap implementációval), Bellman-Ford (negatív élek kezelése, O(VE)), egyszerűsített körmentes gráf eset.  
**Max flow:** Ford–Fulkerson (augmentáló utak, integritás esetén fut), Edmonds–Karp (BFS augmentáló utak; O(VE^2)).  
**Vizsga gyakorlat:** Prim/Kruskal lépéseinek bemutatása; Dijkstra futása konkrét gráfon.

# 7. Redundancia és anomáliák relációs RDBMS-ben. Normalizálás. NoSQL
**Anomáliák:** beszúrási, törlési, frissítési anomáliák példákkal.  
**Funkcionális függőségek:** definíció; teljes, részleges, tranzitív függőség.  
**Normalizálási lépések:** 0NF → 1NF → 2NF → 3NF → BCNF; szabályok és példák a relációk bontására.  
**ACID vs. CAP:** tranzakciós izoláció, tartósság, konzisztencia; CAP tétel elve (Consistency, Availability, Partition tolerance — csak kettő garantálható elosztott rendszerekben).  
**NoSQL rendszerek:** típusok: kulcs-érték, dokumentum, column-family, graf; konzisztenciamodellek (eventual consistency stb.).  
**MapReduce:** paradigma: Map és Reduce lépések, példa szógyakoriság-számolásra.  
**Gyakorlat:** adott normalizációs példa megoldása, osztott rendszer trade-off elemzése.

# 8. Koncepcionális adatbázistervezés, (E)ER modell, relációs algebra, SQL
**ER modell:** entitások, attribútumok, kapcsolatok, erős/gyenge egyedek; kardinalitások.  
**EER:** specializáció/általánosítás, öröklődés, unió típusok.  
**Leképezés relációra:** szabályok különböző kapcsolat- illetve öröklődési esetekre.  
**Relációs algebra:** szelekció, projekció, unió, különbség, természetes join, átlapolás (theta-join), renaming; algebrai műveletek példákkal.  
**SQL:** DDL, DML; SELECT-FROM-WHERE, aggregációk, csoportosítás, JOIN típusok, al-lekérdezések, tranzakciókezelés.  
**Vizsga feladat:** ER-diagramról relációk készítése; SQL-lekérdezés megírása komplex joinokkal és aggregátumokkal.

# 9. Ágensek, logikai ágens, ítéletkalkulus
**Ágens fogalma:** érzékelő, cselekvés, környezet, feladatkörnyezet jellemzői (deterministic/stochastic, fully/partially observable stb.).  
**Ágenstípusok:** reflexív, model-based, cél-orientált, utility-based; multi-agent rendszerek alapjai.  
**Logikai ágens:** tudásbázis + következtetés; formális logikák alkalmazása.  
**Ítéletkalkulus (propositional logic):** szintaxis, szemantika, sat/unsat, tautológia.  
**Tételbizonyítási módszerek:** igazságtábla, Quine-McCluskey (logikai minimalizálás — Quine említése a tételsorban: valószínű a Quine algoritmus itt), formális levezetés, rezolúció (CNF-re hozás, rezolúciós szabály).  
**Gyakorlat:** egyszerű következtetés bizonyítása rezolúcióval; logikai kifejezés CNF-re hozása.

# 10. Problémareprezentáció gráfokkal; keresések; kétszemélyes játékok
**Állapottér modell:** csúcspontok = állapotok, élek = lépések; célállapot definiálása.  
**Keresési algoritmusok:** vak keresések (BFS, DFS, IDS, uniform-cost), heurisztikus (greedy best-first, A*, IDA*), lokális keresők (hill-climbing, simulated annealing).  
**Heurisztika:** konszisztencia, admissibility; A* bizonyítékok.  
**Populációs keresők:** beam search, PSO, genetikus algoritmusok (kódolás, fitness, szelekció, crossover, mutáció).  
**Kétszemélyes játékok:** minimax és alfa-béta vágás; állapotértékelés, mélység-korlátozás.  
**Vizsga feladat:** A* futása adott gráfon heurisztikával; minimax számítása egyszerű játékfán.

# 11. Gépi tanulás fajtái; ismert algoritmusok; neurális hálók
**Felosztás:** felügyelt, nem-felügyelt, félig felügyelt, megerősítéses.  
**Felügyelt tanulás:** regresszió, klasszifikáció; döntési fák, SVM, kNN, Naive Bayes.  
**Nem-felügyelt:** clustering (k-means), asszociációs szabályok.  
**Megerősítéses tanulás:** MDP alapok, aktív vs. passzív RL, Q-learning alapok.  
**Neurális hálózatok:** neuron modellja, aktivációs függvények, architektúrák (MLP, CNN, RNN), veszteségfüggvények, backpropagation, regularizáció (dropout, L2), overfitting és kezelése.  
**Gyakorlat:** egyszerű perceptron tanítása; k-means iterációi; Q-learning frissítési szabály.

# Informatikai tárgycsoport - 1. Informacio reprezentációi (számrendszerek)
**Tartalom:** bináris, hex, oktális; endianitás; egész szám ábrázolás (signed/unsigned, two's complement); fix- és lebegőpontos ábrázolás (IEEE 754 alapok); Hamming-kódolás hibadetektálásra/correktálásra.  
**Vizsga gyakorlat:** konverziók, lebegőpontos szám ábrázolásának dekódolása, egyszerű Hamming-kód hibajavítás.

# 2. ALU felépítése és működése
**Téma:** alapvető logikai építők: fél- és teljes összeadó, soros/párhuzamos összeadás (ripple-carry, carry-lookahead elv); kivonó, szorzó és osztó (alapalgoritmusok).  
**Univerzális teljesség:** NAND/NOR kielégítik a Boole-függvények teljes készletét.  
**Gyakorlat:** egyszerű aritmetikai áramkörök tervezése logikai kapukkal.

# 3. Vezérlő egységek (huzalozott vs. mikroprogramozott)
**Huzalozott (hardwired) vezérlők:** gyorsak, de kevésbé rugalmasak; Mealy és Moore automaták összehasonlítása.  
**Mikroprogramozott vezérlők:** mikro-utasítások, horizontális vs. vertikális mikroprogramozás; előnyök/hátrányok.  
**Gyakorlat:** egyszerű vezérlő állapotgép rajzolása, Mealy vs Moore példával.

# 4. Folyamatok kezelése multiprogramozott rendszerekben
**Fogalmak:** folyamat életciklus, állapotok, kontextusváltás, folyamat vezérlő blokkok (PCB).  
**Ütemezés:** FCFS, SJF, Priority, Round-Robin, Multilevel Queue; metrikák: throughput, turnaround, waiting time.  
**Szinkronizáció:** kritikus szakasz, mutex, szemaforok (P/V műveletek), monitorok.  
**Holtpont:** Coffman feltételek; holtpont megelőzés, elkerülés (Banker algoritmus), feloldás módszerei.  
**Gyakorlat:** szemaforral történő producer-consumer megoldás, holtpont-feltárás példával.

# 5. Tárkezelés korszerű módszerei
**Memóriahierarchia:** cache, fizikai/virtuális memória; címleképezés (bázis-relatív, offset alapú).  
**Virtuális memória:** lapozás (paging), szegmentáció; TLB, page replacement algoritmusok (LRU, FIFO, Optimal).  
**Fragmentáció:** belső és külső problémák; memóriaallokációs stratégiák.  
**Gyakorlat:** LRU vs FIFO összehasonlító feladat, címtranszformáció számítása.

# 6. Háttértárak és kezelésük
**Tároló eszközök:** HDD, SSD alapok; RAID szintek (0,1,5,6 stb.).  
**Fájlrendszer:** inode-ok, blokkok allokációja, szabad blokkok kezelése (bitmap, linked list).  
**Elosztott állománykezelés:** NFS, RPC alapok; konzisztencia kérdések.  
**Gyakorlat:** fájl blokkok allokációs példája, RAID tervezési kérdés.

# 7. Fizikai és adatkapcsolati réteg jellemzése
**Fizikai réteg:** átviteli közegek (vezetékes: UTP, koax, optikai; vezeték nélküli: rádió); fizikai topológiák.  
**Adatkapcsolati réteg:** MAC cím, Ethernet keret struktúra, hibakezelés, hozzáférés-vezérlés (CSMA/CD).  
**Switch működése:** MAC tanulás, frame forwarding, VLAN alapok.  
**Gyakorlat:** Ethernet keret mezőinek értelmezése, CRC szerepe.

# 8. Hálózati réteg (IPv4, IPv6, alhálózatok)
**IPv4/IPv6 címzés:** struktúra, prefix, unicast/multicast/anycast; publikus vs privát címek.  
**VLSM és alhálózat számítás:** CIDR notáció, maszkok, gyakorlati számítások (példa: három alhálózat kiosztása).  
**Útvonalválasztás:** interior vs exterior routing, alap protokollok szerepe.  
**Gyakorlat:** alhálózatok kiszámítása megadott igények alapján.

# 9. Szállítási réteg (TCP/UDP)
**UDP:** connectionless, alacsony overhead, alkalmazások: DNS, VoIP.  
**TCP:** kapcsolat felépítése (3-way handshake), bontás (4-way), portszámok szerepe, megbízhatóság (ACK, retransmission), csúszó ablakos kontroll (flow control), torlódásvezérlés (congestion control alapok — Tahoe, Reno).  
**Gyakorlat:** TCP állapotlegenda és csomaglábjegyzet értelmezése.

# 10. A szoftver, mint termék; szoftvergyártási modellek
**Alapok:** specifikáció, tervezés, implementáció, validáció, karbantartás.  
**Modellek:** vízesés, iteratív, spirális, inkrementális, XP, komponens-alapú fejlesztés; összehasonlításuk előnyökkel/hátrányokkal.  
**Gyakorlat:** modell kiválasztása adott projekthez indoklással.

# 11. Objektumorientált szoftvertervezés és UML
**OOP alapismeretek:** osztály, objektum, öröklődés, polimorfizmus, enkapszuláció.  
**UML-diagramok:** use-case, class, state, activity, sequence; jelölések és tipikus használatuk.  
**RUP:** fázisok (inception, elaboration, construction, transition), nézetek és diszciplinák.  
**Gyakorlat:** egyszerű rendszer UML modellje különböző diagramokkal.

# 12. Szoftvertesztelés alapfogalmai
**Alapok:** verifikáció vs validáció; statikus vs dinamikus tesztelés.  
**Lefedettség:** kód (statement) coverage, branch coverage, decision coverage.  
**Tesztelési módszerek:** black-box (követelmény-alapú, partíciós tesztelés), white-box (út-, feltétel alapú), tesztszintek (unit, integration, system, acceptance).  
**Teszttervezés:** test case írás, teszt adatok kialakítása, hibareprodukció.  
**Gyakorlat:** egyszerű tesztesetek készítése adott specifikációhoz; lefedettség mérés magyarázata.
