# 2. Tétel: Környezetfüggetlen nyelvek (CF nyelvek)

Ez a tétel a reguláris nyelveknél bővebb nyelvosztállyal, a környezetfüggetlen nyelvekkel, azok generálásával (nyelvtanok) és felismerésével (veremautomaták) foglalkozik [1].

## 1. Definíció: Környezetfüggetlen nyelvtan (CFG)
A környezetfüggetlen nyelveket környezetfüggetlen nyelvtanok generálják.
Egy CFG egy $G = (V, \Sigma, R, S)$ rendezett négyes, ahol [2]:
*   **V**: Terminálisok és nemterminálisok (változók) halmaza.
*   **$\Sigma$**: Terminális szimbólumok halmaza (ábécé), $\Sigma \subseteq V$.
*   **R**: Szabályok halmaza. Alakjuk: $A \to \gamma$, ahol $A$ egy nemterminális, $\gamma \in V^*$ (terminálisok és nemterminálisok sorozata).
    *   *Lényeg:* A bal oldalon mindig egyetlen nemterminális áll (ezért környezetfüggetlen).
*   **S**: Kezdőszimbólum ($S \in V \setminus \Sigma$).

**Példa szabály:** $S \to aSb$ (generálja: $ab, aabb, \dots$) [2].

## 2. Felismerés: Veremautomata (PDA)
A CF nyelvek felismerői a veremautomaták (Pushdown Automata).
*   **Működés:** Ez egy véges automata, kiegészítve egy **veremmel** (stack, LIFO memória). Az automata a verem tetejét olvashatja és írhatja [3].
*   **Formálisan:** 7-es (állapotok, bemeneti ábécé, verem ábécé, átmeneti reláció, kezdőállapot, verem kezdőszimbólum, végállapotok).
*   **Determinisztikus vs. Nem-determinisztikus:** A CF nyelveknél a *nem-determinisztikus* veremautomata (NPDA) kifejezőereje nagyobb, mint a determinisztikusé (szemben a véges automatákkal, ahol DFA = NFA).

## 3. Eszközök ekvivalenciája (CFG $\leftrightarrow$ PDA)
A tétel egyik központi állítása, hogy a környezetfüggetlen nyelvtanok és a (nem-determinisztikus) veremautomaták ekvivalensek.

### CFG $\to$ PDA konstrukció
Minden CFG-hez készíthető olyan PDA, amely ugyanazt a nyelvet ismeri fel.
*   **Módszer:** A PDA a veremben szimulálja a nyelvtan **baloldali levezetését** (leftmost derivation) [4].
*   **Működés:**
    1.  A veremben a nemterminálisokat a szabályok jobb oldalára cseréljük (pl. ha van $A \to w$ szabály, akkor $A$-t $w$-re cseréljük).
    2.  Ha a verem tetején terminális van, összehasonlítjuk a bemenettel. Ha egyezik, mindkettőt "fogyasztjuk" (léptetjük) [5].

## 4. Zártsági tételek
A környezetfüggetlen nyelvek osztályára vonatkozó műveleti tulajdonságok [6]:
*   **Zárt:** Unió ($\cup$), Konkatenáció (összefűzés), Kleene-csillag (*).
*   **NEM Zárt:** Metszet ($\cap$), Komplementer (kiegészítés).
    *   *Megjegyzés:* Egy környezetfüggetlen és egy reguláris nyelv metszete mindig környezetfüggetlen [6].

## 5. A második pumpálási lemma (CF nyelvekre)
Ezzel bizonyítható, hogy egy nyelv **NEM** környezetfüggetlen (pl. $a^n b^n c^n$).
*   **Tétel:** Ha $L$ környezetfüggetlen, akkor minden elég hosszú $w \in L$ szó felbontható öt részre: $w = uvxyz$, ahol:
    1.  $vy \neq \epsilon$ (legalább az egyik pumpálható rész nem üres).
    2.  Bármely $i \ge 0$ esetén $uv^ixy^iz \in L$ (a $v$ és $y$ részeket egyszerre pumpálva is a nyelvben maradunk) [3].
# 3. Tétel: Turing elfogadható nyelvek

Ez a tétel a számításelmélet legerősebb modelljét, a Turing-gépet, valamint az algoritmikus megoldhatóság határait (eldönthetőség vs. elfogadhatóság) tárgyalja.

## 1. Turing-gép (TM) definíciója
A Turing-gép a digitális számítógépek absztrakt matematikai modellje.
*   **Felépítése:** Egy véges állapotú vezérlőegység és egy jobbra végtelen szalag.
*   **Formálisan:** $M = (K, \Sigma, \delta, s, H)$ ötös, ahol:
    *   $K$: Állapotok véges halmaza.
    *   $\Sigma$: Szalag ábécé (tartalmazza a speciális $\rhd$ start és $\sqcup$ üres szimbólumokat).
    *   $s$: Kezdőállapot ($s \in K$).
    *   $H$: Megállási állapotok halmaza ($H \subseteq K$).
    *   $\delta$: Átmeneti függvény. $(K \setminus H) \times \Sigma \rightarrow K \times (\Sigma \cup \{\leftarrow, \rightarrow\})$.
        *   A gép olvas egy jelet, majd: új állapotba lép, új jelet ír a szalagra VAGY elmozdítja a fejet (balra/jobbra) [1][2].

### Különbség a veremautomatához (PDA) képest
1.  **Memória:** A TM-nek nincs verme, helyette a szalagra írhat és onnan olvashat (a szalag a memória) [3][4].
2.  **Mozgás:** A TM olvasófeje balra is mozoghat, nem csak jobbra [3].
3.  **Determinisztikus:** Az alapértelmezett TM determinisztikus [5][6].

### Végállapot vs. Megállási állapot
*   **Megállási állapot (Halting state):** Ha a gép ebbe kerül, a működés leáll. Ez nem feltétlenül jelent elfogadást, csak a számítás végét [7].
*   **Elfogadás:** Egy $w$ szó akkor van elfogadva, ha a gép elfogadó állapotban áll meg.

## 2. Machine Schema (Gép sémák)
Mivel a TM állapotátmenet-táblával történő leírása bonyolult, **Machine Schemákat** használunk, amelyek elemi Turing-gépekből épülnek fel [8][9].
*   **Elemi gépek:** Jobbra lépés ($R$), Balra lépés ($L$), Szimbólum írása ($a$) [10].
*   **Nevezetes sémák:**
    *   **Másoló gép (Copy, $C$):** $ \sqcup w \sqcup \rightarrow \sqcup w \sqcup w \sqcup $ (megkettőzi a bemenetet) [11][12].
    *   **Shiftelő gép ($S$):** $ \sqcup w \sqcup \rightarrow \sqcup \sqcup w \sqcup $ (eltolja a szót jobbra) [13][14].
    *   **Eldöntő gépek:** Pl. az $L = \{a^n b^n c^n\}$ nyelvet felismerő gép (amit PDA nem tud) [14].

## 3. Nyelvosztályok: Elfogadható vs. Eldönthető
A tétel központi része a megoldhatóság szintjeinek megkülönböztetése.

### Turing-elfogadható (Turing acceptable / Recursively enumerable)
Egy $L$ nyelv Turing-elfogadható, ha létezik olyan $M$ gép, amely:
*   Ha $w \in L$: A gép megáll és elfogadja.
*   Ha $w \notin L$: A gép **vagy** megáll és elutasítja, **vagy** végtelen ciklusba kerül (sosem áll meg) [15][16].

### Turing-eldönthető (Turing decidable / Recursive)
Egy $L$ nyelv Turing-eldönthető (rekurzív), ha létezik olyan $M$ gép, amely:
*   Minden bemenetre ($w$) garantáltan **megáll** véges időn belül.
*   Kimenete egyértelmű IGEN ($Y$) vagy NEM ($N$) válasz [17][18].
*   *Kapcsolat:* Minden eldönthető nyelv elfogadható is, de fordítva nem igaz [18].

### Karakterisztikus függvény
Az $L$ nyelv karakterisztikus függvénye ($\chi_L$) 1 (vagy Y) értéket ad, ha $w \in L$, és 0 (vagy N) értéket, ha $w \notin L$. Egy nyelv akkor eldönthető, ha a karakterisztikus függvénye kiszámítható [19][20].

## 4. Church-Turing tézis
Nem matematikai tétel, hanem egy hipotézis:
*   Minden olyan probléma, ami intuitív értelemben "kiszámítható" vagy "algoritmizálható", megoldható Turing-géppel is.
*   A Turing-gép a létező legerősebb számítási modell (a mai modern számítógépekkel ekvivalens erejű) [21][14].

## 5. Univerzális Turing-gép és a Megállási probléma
*   **Univerzális Turing-gép (UTM):** Egy olyan gép, amely képes szimulálni bármely más Turing-gépet. Bemenete egy tetszőleges $M$ gép kódja és egy $w$ bemenet [22][23].
*   **Megállási probléma (Halting Problem):**
    *   *Kérdés:* Létezik-e olyan algoritmus, amely egy tetszőleges $M$ Turing-gépről és $w$ bemenetről eldönti, hogy $M$ megáll-e $w$-n?
    *   *Válasz:* **NEM.** A probléma bizonyítottan eldönthetetlen (undecidable). Nincs olyan gép, ami minden esetre helyes választ adna végtelen ciklus nélkül [24][25].
    *   *Bizonyítás:* Diagonalizációs elvvel történik.

# 4. Tétel: Algoritmus futási ideje, rendező és kereső algoritmusok

Ez a tétel az algoritmusok bonyolultságának matematikai leírását (aszimptotikus jelölések), valamint a különböző hatékonyságú rendezési és keresési módszereket tárgyalja [1], [2].

## 1. Algoritmus futási ideje (Aszimptotikus jelölések)
Az algoritmusok hatékonyságát a bemenet méretének ($n$) függvényében vizsgáljuk. A pontos lépésszám helyett a **növekedési rendet** (nagyságrendet) határozzuk meg [3].

### Jelölések [3]:
*   **$O(g(n))$ (Nagy Ordó) – Felső korlát:** Az algoritmus lépésszáma "legfeljebb" $c \cdot g(n)$. A legrosszabb eset (worst-case) jellemzésére használjuk.
    *   Definíció: $\exists c > 0, n_0 \ge 0$, hogy $\forall n \ge n_0 : f(n) \le c \cdot g(n)$.
*   **$\Omega(g(n))$ (Nagy Omega) – Alsó korlát:** Az algoritmus lépésszáma "legalább" $c \cdot g(n)$. A legjobb eset (best-case) jellemzésére használjuk.
*   **$\Theta(g(n))$ (Nagy Théta) – Szoros korlát:** Az algoritmus pontos nagyságrendje (alulról és felülről is korlátoz). Átlagos eset jellemzésére gyakran ezt használjuk [4].

### Bonyolultsági osztályok (növekvő sorrendben) [3]:
1.  **Konstans:** $O(1)$
2.  **Logaritmikus:** $O(\log n)$ (pl. bináris keresés)
3.  **Lineáris:** $O(n)$ (pl. lineáris keresés)
4.  **Linearitmikus:** $O(n \log n)$ (pl. gyors rendezések)
5.  **Négyzetes:** $O(n^2)$ (pl. egyszerű rendezések)
6.  **Exponenciális:** $O(2^n)$ (gyakorlatilag megoldhatatlan nagy $n$-re).

## 2. Négyzetes rendező algoritmusok ($O(n^2)$)
Ezek egyszerű, de lassú algoritmusok. Általában stabilak (kivéve a minimum kiválasztást) és helyben rendeznek.

*   **Buborékrendezés (Bubble Sort):**
    *   *Működés:* Szomszédos elemeket hasonlít össze és cserél, ha rossz sorrendben vannak. Minden menetben a legnagyobb elem "felbuborékol" a helyére [5].
    *   *Stabilitás:* Stabil.
*   **Beszúró rendezés (Insertion Sort):**
    *   *Működés:* A tömböt egy rendezett és egy rendezetlen részre osztja. A rendezetlen rész első elemét veszi, és a rendezett részben a megfelelő helyre szúrja be (az elemeket jobbra tolva) [6].
    *   *Előny:* Kis méretű vagy majdnem rendezett tömböknél nagyon hatékony.
*   **Minimum kiválasztásos rendezés (Selection Sort):**
    *   *Működés:* Megkeresi a tömb legkisebb elemét és kicseréli az elsővel. Majd a maradékból keresi a legkisebbet, stb. [7].
    *   *Stabilitás:* Nem stabil.

## 3. Gyorsabb rendező algoritmusok ($O(n \log n)$)
Ezek alkalmasak nagy adatmennyiség rendezésére.

*   **Gyorsrendezés (Quick Sort):**
    *   *Elv:* "Oszd meg és uralkodj". Kiválaszt egy **pivot** elemet. A tömböt két részre osztja: a pivotnál kisebbekre és nagyobbakra. Rekurzívan rendezi a részeket [8].
    *   *Bonyolultság:* Átlagosan $O(n \log n)$, de legrosszabb esetben $O(n^2)$ (ha rossz a pivot választás). Nem stabil.
*   **Összefésülő rendezés (Merge Sort):**
    *   *Elv:* "Oszd meg és uralkodj". A tömböt felezi addig, amíg 1 elemű részeket kap. Majd a rendezett részeket **összefésüli** (merge) egy nagyobb rendezett tömbbé [9].
    *   *Bonyolultság:* Garantált $O(n \log n)$. Stabil.
*   **Kupacrendezés (Heap Sort):**
    *   *Működés:* A tömbből egy **kupac** (heap) adatszerkezetet épít (ahol a gyökér a legnagyobb elem). A gyökeret kiveszi és a tömb végére teszi, majd helyreállítja a kupac tulajdonságot [10].
    *   *Bonyolultság:* Garantált $O(n \log n)$. Nem stabil.

## 4. Lineáris idejű rendezések (Speciális esetek)
Nem összehasonlításon alapulnak, ezért gyorsabbak lehetnek $O(n \log n)$-nél, de korlátozott a bemenetük.

*   **Leszámláló rendezés (Counting Sort):** Egész számokra, szűk intervallumon. Megszámolja az egyes elemek előfordulását, majd pozícióba helyezi őket. Idő: $O(n+k)$ [9].
*   **Számjegyes rendezés (Radix Sort):** Számjegyek (vagy karakterek) szerint rendez, a legkisebb helyiértéktől a legnagyobbig (LSD). Stabilnak kell lennie a belső rendezésnek. Idő: $O(d \cdot (n+k))$ [11].
*   **Edényrendezés (Bucket Sort):** Az elemeket intervallumokba (vödrökbe) osztja, a vödröket külön rendezi, majd összefűzi őket [12].

## 5. Kereső algoritmusok
*   **Lineáris keresés (Szekvenciális):** Végigmegy a listán elejétől a végéig.
    *   *Feltétel:* Nincs (rendezetlen tömbre is működik).
    *   *Idő:* $O(n)$ [13].
*   **Bináris keresés (Logaritmikus):** A középső elemet vizsgálja. Ha a keresett érték kisebb, a bal oldali résztömbben, ha nagyobb, a jobb oldaliban folytatja a keresést.
    *   *Feltétel:* **Rendezett** tömb szükséges.
    *   *Idő:* $O(\log n)$ [14].

# 5. Tétel: Elemi és fejlett adatszerkezetek

Ez a tétel az adatok rendszerezett tárolását, a műveletek hatékonyságát (beszúrás, törlés, keresés) és a különböző absztrakt adattípusok implementációját foglalja össze.

## 1. Elemi adatszerkezetek
Ezek az alapvető tárolók, amelyek speciális szabályok szerint kezelik az elemek sorrendjét.

*   **Verem (Stack):**
    *   **Elv:** LIFO (Last In, First Out) – Utoljára be, először ki.
    *   **Műveletek:** *Push* (betesz), *Pop* (kivesz), *Top/Peek* (felső elem olvasása), *IsEmpty*,.
    *   **Használat:** Függvényhívások kezelése, veremautomaták.
    *   **Bonyolultság:** Minden művelet $O(1)$.
*   **Sor (Queue):**
    *   **Elv:** FIFO (First In, First Out) – Elsőként be, elsőként ki.
    *   **Műveletek:** *Enqueue* (sor végére tesz), *Dequeue* (sor elejéről vesz), *First*, *IsEmpty*,.
    *   **Használat:** Ütemezők, pufferek.
    *   **Bonyolultság:** Minden művelet $O(1)$.
*   **Láncolt listák (Linked Lists):**
    *   Lineáris adatszerkezet, ahol az elemek (csomópontok) mutatókkal kapcsolódnak egymáshoz. Nem folytonos a memóriában.
    *   **Típusai:** Egyszeresen láncolt (csak előre mutat), Kétszeresen láncolt (előre és hátra is mutat), Cirkuláris (az utolsó elem az elsőre mutat), Fejelemes (sentinel node).
    *   **Bonyolultság:** Beszúrás/Törlés ismert pozíciónál $O(1)$, Keresés $O(n)$,.

## 2. Bináris keresőfák (BST)
Olyan bináris fa, amelyre igaz a **keresőfa tulajdonság**: minden csúcsra a bal oldali részfában csak kisebb, a jobb oldaliban csak nagyobb kulcsok vannak,.
*   **Adatszerkezet:** Mutató a szülőre ($p$), bal gyerekre ($left$) és jobb gyerekre ($right$).
*   **Bejárások:**
    *   *Inorder:* Bal $\to$ Gyökér $\to$ Jobb (rendezett sorrendet ad).
    *   *Preorder:* Gyökér $\to$ Bal $\to$ Jobb.
    *   *Postorder:* Bal $\to$ Jobb $\to$ Gyökér,.
*   **Műveletek ideje:** Az alapműveletek (keresés, minimum, maximum, beszúrás, törlés) a fa magasságával ($h$) arányosak.
    *   Átlagos eset: $O(\log n)$.
    *   Legrosszabb eset (elfajult fa, lánc): $O(n)$.

## 3. Kiegyensúlyozott és speciális fák
A BST hátrányainak (elfajulás) kiküszöbölésére szolgáló struktúrák, melyek garantálják a logaritmikus magasságot.

*   **Kupac (Heap):**
    *   Bináris fa alapú, tömbben ábrázolt struktúra.
    *   **Tulajdonság (Max-Heap):** A szülő értéke mindig $\ge$ a gyerekek értékeinél (a gyökér a legnagyobb),.
    *   **Műveletek:** *Heapify* (helyreállítás), *Insert*, *ExtractMax*.
    *   **Használat:** Prioritásos sorok, Kupacrendezés.
*   **Piros-fekete fák (Red-Black Trees):**
    *   Kiegyensúlyozott bináris keresőfa, ahol minden csúcsnak van egy színe (piros vagy fekete).
    *   **Tulajdonságok:** Gyökér fekete; Levél (NIL) fekete; Piros csúcs gyereke fekete; Minden úton ugyanannyi fekete csúcs van (fekete-magasság),.
    *   **Előny:** A magasság legfeljebb $2\log(n+1)$, így a műveletek garantáltan $O(\log n)$ idejűek. Beszúráskor/törléskor színcserékkel és **forgatásokkal** állítja helyre az egyensúlyt.
*   **B-fák (B-Trees):**
    *   Kiegyensúlyozott keresőfa, ahol egy csúcsnak *több* kulcsa és *több* gyereke lehet (magas elágazási tényező).
    *   **Jellemzők:** Minden levél azonos mélységben van. Egy $k$ kulcsot tartalmazó csúcsnak $k+1$ gyereke van,.
    *   **Használat:** Háttértárolók (lemez) és adatbázisok indexelésére optimalizálva (ritka lemezművelet).

## 4. Hasító táblázatok (Hash Tables)
Kulcs-érték párok tárolására szolgáló struktúra, amely a kulcsot egy **hasítófüggvény** ($h(k)$) segítségével képezi le egy tömbindexre.
*   **Hatékonyság:** Konstans idejű $O(1)$ keresés, beszúrás és törlés (átlagos esetben),.
*   **Hasítófüggvények:** Cél az egyenletes eloszlás. Módszerek: *Osztásos* ($k \pmod m$), *Szorzásos*.
*   **Ütközéskezelés (Collision resolution):** Ha két kulcs ugyanoda képződik le:
    1.  **Láncolás (Chaining):** Az azonos indexű elemeket egy láncolt listába fűzzük.
    2.  **Nyílt címzés (Open addressing):** Minden elem a táblázatban van. Ha a hely foglalt, keresünk egy másikat.
        *   *Lineáris próba:* Következő szabad hely.
        *   *Négyzetes próba:* Ugrás négyzetszámokkal.
        *   *Dupla hasítás:* Második hash függvény használata a lépésközhöz,.

# 6. Tétel: Gráf algoritmusok

Ez a tétel a gráfok reprezentációját, bejárási stratégiáit (szélességi, mélységi), valamint a legfontosabb optimalizálási problémákat (feszítőfák, legrövidebb utak, maximális folyam) tárgyalja.

## 1. Gráfok ábrázolása
A gráfok tárolásának két alapvető módja van a memóriában:
*   **Szomszédsági mátrix:** $V \times V$ méretű mátrix. $A[i][j] = 1$ (vagy a súly), ha van él $i$-ből $j$-be. Előnye a gyors élkeresés $O(1)$, hátránya a nagy tárigény $O(V^2)$, ritka gráfoknál pazarló.
*   **Szomszédsági lista:** Minden csúcshoz egy láncolt lista tartozik, amely a szomszédos csúcsokat tartalmazza. Tárigénye $O(V+E)$, ami ritka gráfoknál ideális.

## 2. Gráf bejárások
A gráf csúcsainak szisztematikus meglátogatása.
*   **Szélességi keresés (BFS - Breadth-First Search):**
    *   **Működés:** A kezdőcsúcstól indulva rétegenként halad (először a közvetlen szomszédokat, majd azok szomszédait látogatja). **FIFO** (Sor) adatszerkezetet használ.
    *   **Tulajdonság:** Súlyozatlan gráfban megtalálja a legrövidebb utat (élek száma szerint) a kezdőpontból.
    *   **Időigény:** $O(V+E)$ (szomszédsági listával),.
*   **Mélységi keresés (DFS - Depth-First Search):**
    *   **Működés:** Egy ágon amilyen mélyre csak lehet, elmegy, majd visszalép (backtrack). **LIFO** (Verem) adatszerkezetet vagy rekurziót használ.
    *   **Időbélyegek:** Minden csúcshoz rögzíti a *felfedezési* (szürke lesz) és *befejezési* (fekete lesz) időt. Ezekkel osztályozhatók az élek (fa-, vissza-, előre-, keresztél).
    *   **Időigény:** $O(V+E)$,.

## 3. Minimális feszítőfák (MST)
Cél: Egy összefüggő, súlyozott gráf összes csúcsának összekötése úgy, hogy az élek összsúlya minimális legyen, és ne keletkezzen kör.
*   **Kruskal algoritmusa:**
    *   „Mohó” stratégia: Az éleket súlyuk szerint növekvő sorrendbe rendezi.
    *   Mindig a legkisebb súlyú élt választja, amely nem alkot kört a már kiválasztottakkal (Unió-Holvan adatszerkezettel hatékony).
    *   Addig megy, amíg $V-1$ élt ki nem választott,.
*   **Prim algoritmusa:**
    *   Egy tetszőleges kezdőcsúcsból növeszti a fát.
    *   Minden lépésben azt a legkisebb súlyú élt adja hozzá, amely a fa egyik csúcsát köti össze egy fán kívüli csúccsal,.

## 4. Legrövidebb utak (Egy forrásból)
Adott $s$ kezdőcsúcsból keressük a legrövidebb utat az összes többi csúcsba.
*   **Dijkstra algoritmusa:**
    *   **Feltétel:** Nem lehetnek negatív súlyú élek.
    *   **Működés:** Mohó stratégia. Mindig a legkisebb becsült távolságú, még nem kész csúcsot választja, és „relaxálja” (javítja) a szomszédai távolságát. Prioritásos sort használ.
    *   **Időigény:** $O(E \log V)$ vagy $O(V^2)$ implementációtól függően,.
*   **Bellman-Ford algoritmus:**
    *   **Előny:** Kezeli a **negatív** súlyú éleket is.
    *   **Működés:** $V-1$-szer megy végig az összes élen és relaxálja őket. Képes detektálni a negatív összsúlyú köröket (ha a $V$. iterációban is tud javítani, akkor van negatív kör).
    *   **Időigény:** $O(V \cdot E)$,,.
*   **Körmentes irányított gráfok (DAG):**
    *   Ha a gráfban nincs kör, a csúcsok **topologikus sorrendje** szerinti egyszeri relaxálás elegendő. Ez lineáris időben fut: $O(V+E)$,.

## 5. Maximális folyam (Maximum Flow)
Adott egy irányított gráf kapacitásokkal, egy forrás ($s$) és egy nyelő ($t$) csúcs. Mennyi a maximális anyagmennyiség, ami átküldhető?
*   **Ford-Fulkerson módszer:**
    *   **Működés:** Javítóutakat (augmenting path) keres a *reziduális* (maradék) hálózatban $s$-ből $t$-be.
    *   Amíg talál utat, a folyamot megnöveli az út „szűk keresztmetszetével” (a legkisebb kapacitással az úton).
    *   Akkor áll meg, ha nincs több javítóút.
    *   **Edmonds-Karp algoritmus:** A Ford-Fulkerson egy implementációja, ahol a javítóutat BFS-sel (legkevesebb él) keresi. Időigénye $O(V E^2)$,.

# 7. Tétel: Redundancia, normalizálás és NoSQL rendszerek

Ez a tétel a relációs adatbázisok tervezési hibáinak (redundancia) kiküszöbölésével, a normalizálás lépéseivel, valamint a relációs modell korlátainak átlépésével (NoSQL) foglalkozik.

## 1. Redundancia és anomáliák
A **redundancia** a többszörös, felesleges adattárolást jelenti. Ez nemcsak tárhelypazarló, hanem **anomáliákhoz** (rendellenességekhez) vezet az adatbázis-műveletek során, ami inkonzisztenciát okozhat [1].

### Az anomáliák típusai (Példákkal)
1.  **Beszúrási anomália (Insertion anomaly):**
    *   Nem tudunk rögzíteni egy adatot, mert hiányzik egy másik, hozzá kapcsolódó adat, ami a kulcs része lenne.
    *   *Példa:* Egy `KURZUS` táblában nem tudunk felvenni új tantárgyat, amíg nincs hallgató, aki felvette volna (ha a hallgató is része a kulcsnak) [2], [3].
2.  **Módosítási anomália (Update anomaly):**
    *   Ha egy adat többször szerepel, és módosításkor nem minden előfordulását írjuk át, az adatbázis ellentmondásossá válik.
    *   *Példa:* Ha egy tanár címe megváltozik, és ez minden általa tartott kurzusnál külön tárolva van, az összes sort módosítani kell [4], [5].
3.  **Törlési anomália (Deletion anomaly):**
    *   Egy rekord törlésekor olyan információ is elveszik, amit meg szerettünk volna őrizni.
    *   *Példa:* Ha töröljük az egyetlen hallgatót egy kurzusról, és a kurzus adatai is ugyanabban a sorban vannak, a kurzus is törlődik az adatbázisból [2], [6].

## 2. Funkcionális függőségek
A normalizálás alapja a függőségek felismerése. Jelölése: $X \to Y$ (X meghatározza Y-t) [7], [8].

*   **Funkcionális függőség:** Ha $X$ értéke egyértelműen meghatározza $Y$ értékét (pl. *SzemélyiSzám $\to$ Név*).
*   **Teljes funkcionális függőség:** Ha $Y$ függ $X$-től, de $X$ egyetlen valódi részhalmazától sem függ. (Lényeges összetett kulcsoknál).
*   **Részleges függőség:** Ha $Y$ függ egy összetett kulcsnak csak egy részétől (pl. *{Rendszám, Dátum} $\to$ Típus* esetén a *Típus* csak a *Rendszám*-tól függ) [9].
*   **Tranzitív függőség:** Ha $X \to Y$ és $Y \to Z$ (és $Y$ nem határozza meg $X$-et), akkor $X \to Z$ tranzitív módon teljesül (pl. *Hallgató $\to$ Szak $\to$ Kar*) [10], [11].

## 3. Normalizálás (Normál formák)
A normalizálás egy dekompozíciós (szétbontó) eljárás, amely során a táblákat kisebb, jól szerkesztett táblákra bontjuk a redundancia megszüntetése érdekében [12], [13].

*   **0NF (Normalizálatlan):** A tábla ismétlődő csoportokat tartalmaz (pl. egy mezőben több érték) [14].
*   **1NF (Első normálforma):**
    *   Minden mező **atomi** (egyértékű).
    *   Van elsődleges kulcs [15], [16].
*   **2NF (Második normálforma):**
    *   1NF teljesül.
    *   **Nincs részleges függőség**: Minden nem kulcs attribútum a *teljes* elsődleges kulcstól függ (nem csak egy részétől) [10], [16].
*   **3NF (Harmadik normálforma):**
    *   2NF teljesül.
    *   **Nincs tranzitív függőség**: A nem kulcs attribútumok csak a kulcstól függnek, egymástól nem [11], [17].
*   **BCNF (Boyce-Codd normálforma):**
    *   Szigorúbb 3NF. Minden determinánsnak (ami meghatároz egy másik mezőt) szuperkulcsnak kell lennie. Kezeli azokat az eseteket is, ahol a kulcsjelöltek átfedik egymást [18], [19].

## 4. NoSQL rendszerek vs. Relációs modell
A NoSQL ("Not only SQL") rendszerek a Big Data és a nagy skálázhatósági igények miatt jöttek létre, szakítva a szigorú relációs modellel [20], [21].

### ACID vs. CAP
*   **Relációs (RDBMS):** **ACID** elveket követ (Atomiság, Konzisztencia, Izoláció, Tartósság). A tranzakciók mindenáron garantálják az adatbázis épségét [22], [23].
*   **NoSQL:** **CAP tétel** (Brewer-tétel) érvényesül. Elosztott rendszerekben a három tulajdonságból egyszerre csak kettő garantálható [24], [25]:
    1.  **C**onsistency (Konzisztencia - mindenki ugyanazt látja).
    2.  **A**vailability (Rendelkezésre állás - mindig van válasz).
    3.  **P**artition Tolerance (Partíciótűrés - hálózati szakadás esetén is működik).
    *   *Jellemző NoSQL választás:* AP vagy CP (a relációs a CA-ra törekszik, de partíciótűrés nélkül nem elosztott).

### Skálázhatóság
*   **Vertikális (Scale-up):** Erősebb vasat teszünk a szerver alá (RDBMS jellemzője). Korlátos és drága.
*   **Horizontális (Scale-out):** Több olcsó gépet kapcsolunk össze (NoSQL jellemzője). Lineárisan skálázható [26], [27].

## 5. NoSQL típusok és MapReduce
A NoSQL adatbázisokat adatmodelljük szerint csoportosítjuk [20], [28]:

1.  **Kulcs-érték tárolók (Key-Value):** Egyszerű, gyors, skálázható (pl. Redis, Dynamo).
2.  **Oszlopcsaládok (Column-family):** Oszlop-orientált tárolás, nagy adatmennyiséghez (pl. Cassandra, HBase).
3.  **Dokumentum tárolók:** JSON/XML alapú, flexibilis séma (pl. MongoDB, CouchDB).
4.  **Gráf adatbázisok:** Csomópontok és élek, kapcsolatok kezelésére (pl. Neo4j).

### MapReduce
Egy programozási modell nagy adathalmazok elosztott feldolgozására [29].
*   **Map:** A bemenetet kulcs-érték párokká alakítja és szűri/rendezi.
*   **Shuffle:** A kulcsok szerinti csoportosítás.
*   **Reduce:** Az azonos kulcsú adatok aggregálása (pl. összegzés) a végeredmény előállításához.

# 8. Tétel: Koncepcionális adatbázistervezés, (E)ER modell, Relációs algebra és SQL

Ez a tétel az adatbázisok tervezésének elméleti modelljét (ER), annak kiterjesztését (EER), ezek relációs adatbázissá való átalakítását, valamint az adatkezelés matematikai (relációs algebra) és gyakorlati (SQL) nyelveit tárgyalja.

## 1. Koncepcionális tervezés: Az ER modell
Az Egyed-Kapcsolat (Entity-Relationship) modell az adatok magas szintű, implementáció-független ábrázolása, amely a valós világot egyedek és kapcsolatok halmazaként írja le,[1],[2].

### Alapfogalmak
*   **Egyed (Entity):** A valós világ megkülönböztethető objektuma (pl. *Dolgozó*, *Projekt*).
    *   **Erős egyed:** Van saját kulcsa.
    *   **Gyenge egyed:** Nincs saját kulcsa, létezése egy tulajdonos egyedtől függ (pl. *Hozzátartozó*), azonosításához a tulajdonos kulcsa is kell,[3],[4].
*   **Attribútum (Tulajdonság):** Az egyedeket leíró adat.
    *   *Típusai:* Egyszerű, Összetett (pl. Cím), Többértékű (pl. Telefonszámok), Származtatott (pl. Kor), Kulcs (egyedi azonosító),[5],[6],[7].
*   **Kapcsolat (Relationship):** Egyedek közötti viszony.
    *   **Fokszám:** Hány egyed vesz részt benne (Bináris, Terner, n-ágú),[8].
    *   **Kardinalitás (Számosság):**
        *   *1:1 (Egy az egyhez):* Pl. Osztályvezető – Osztály.
        *   *1:N (Egy a sokhoz):* Pl. Osztály – Dolgozó.
        *   *M:N (Sok a sokhoz):* Pl. Hallgató – Kurzus,[9],[10].
    *   **Részvétel:**
        *   *Totális:* Minden egyednek részt kell vennie a kapcsolatban.
        *   *Parciális:* Nem kötelező a részvétel,[11],[12].

## 2. A Kiterjesztett (EER) modell
Az EER (Enhanced ER) modell az objektumorientált tervezéshez hasonló fogalmakkal bővíti az ER modellt a komplexebb összefüggések leírására,[13],[14].

*   **Öröklődés (Főosztály/Alosztály):** Az alosztály (Subclass) örökli a főosztály (Superclass) attribútumait és kapcsolatait (IS-A kapcsolat),[15],[16].
*   **Specializáció / Általánosítás:**
    *   *Specializáció:* Fentről lefelé haladó finomítás (pl. Dolgozó $\to$ Titkárnő, Mérnök).
    *   *Általánosítás:* Alulról felfelé haladó összevonás (pl. Autó, Teherautó $\to$ Jármű),[17],[18].
*   **Korlátozások (Constraints):**
    *   *Elkülönülő (Disjoint):* Egy egyed legfeljebb egy alosztályba tartozhat.
    *   *Átfedő (Overlapping):* Egy egyed több alosztálynak is tagja lehet.
    *   *Teljes (Total) vs. Részleges:* Minden főosztálybeli elemnek be kell-e tartoznia valamelyik alosztályba,[19],[20].
*   **Kategória (Unió típus):** Olyan alosztály, amelynek több, különböző típusú főosztálya van (pl. egy *Tulajdonos* lehet *Személy*, *Bank* vagy *Vállalat*),[21],[22].

## 3. Relációs leképezés (Mapping)
A koncepcionális terv (ER) átalakítása logikai sémává (táblák, kulcsok),[23].

1.  **Erős egyed:** Külön reláció (tábla), attribútumai az oszlopok, kulcsa az elsődleges kulcs (PK),[24].
2.  **Gyenge egyed:** Külön reláció, de tartalmazza a tulajdonos PK-ját idegen kulcsként (FK). A PK a saját parciális kulcsa + a tulajdonos FK-ja,[25].
3.  **1:N kapcsolat:** Az N-oldali táblába felvesszük az 1-oldali tábla PK-ját idegen kulcsként (pl. a Dolgozó táblába az Osztály ID-t),[26].
4.  **M:N kapcsolat:** Új kapcsolótáblát hozunk létre, amely mindkét egyed PK-ját tartalmazza idegen kulcsként (ezek együtt alkotják a kapcsolótábla PK-ját),[27].
5.  **Többértékű attribútum:** Külön táblába kerül (pl. *SzemélyID, Telefonszám*),[28].

## 4. Relációs algebra
A relációs adatbázisok formális, procedurális lekérdező nyelve. Műveletei relációkon (halmazokon) dolgoznak és relációt adnak eredményül,[29],[30].

### Alapműveletek
*   **Szelekció (Kiválasztás, $\sigma$):** Sorok szűrése feltétel alapján ($\sigma_{feltétel}(R)$),[31],[30].
*   **Projekció (Vetítés, $\pi$):** Oszlopok kiválasztása ($\pi_{oszlopok}(R)$). A duplikált sorokat eltávolítja,[32],[33].
*   **Direkt szorzat (Descartes-szorzat, $\times$):** Két tábla minden sorának párosítása ($R \times S$). Eredménye hatalmas méretű lehet,[34],[33].
*   **Unió ($\cup$):** Két unió-kompatibilis (azonos szerkezetű) reláció sorainak egyesítése,[35],[33].
*   **Különbség ($-$):** Azok a sorok, amelyek az elsőben benne vannak, de a másodikban nem,[36],[37].

### Származtatott műveletek
*   **Metszet ($\cap$):** Közös sorok. $R \cap S = R - (R - S)$,[36].
*   **Join (Összekapcsolás, $\bowtie$):** Két tábla összekapcsolása feltétel alapján. Lényegében Descartes-szorzat + Szelekció.
    *   *Natural Join ($*$):* Azonos nevű oszlopok mentén kapcsol össze,[38].
*   **Osztás ($\div$):** "Minden" típusú kérdésekre (pl. kik azok, akik *minden* tárgyat felvettek?),[39].

## 5. SQL (Structured Query Language)
A relációs adatbázisok szabványos nyelve. Deklaratív (azt mondjuk meg, mit akarunk, nem azt, hogy hogyan),[40].

*   **DDL (Data Definition Language):** Adatbázis szerkezetének definiálása.
    *   `CREATE`, `ALTER`, `DROP` (táblák, indexek létrehozása/módosítása),[41].
*   **DML (Data Manipulation Language):** Adatok kezelése.
    *   `INSERT` (beszúrás), `UPDATE` (módosítás), `DELETE` (törlés),[41],[37].
*   **DQL (Data Query Language):** Lekérdezés.
    *   `SELECT ... FROM ... WHERE` (Projekció, Descartes-szorzat/Join, Szelekció),[41].
    *   Csoportosítás: `GROUP BY`, `HAVING` (aggregálás),[42].

# 9. Tétel: Ágensek, ágenstípusok és logika

Ez a tétel a mesterséges intelligencia alapépítőköveit, az ágenseket, azok környezetét és típusait, valamint a tudásreprezentáció és következtetés alapjául szolgáló ítéletkalkulust tárgyalja.

## 1. Az ágens fogalma
Az **ágens** (agent) minden olyan rendszer, amely **érzékelői** (sensors) segítségével észleli a környezetét, és **beavatkozói** (actuators) segítségével cselekszik azon, megváltoztatva azt [1], [2].
*   **Példák:**
    *   *Ember:* Érzékelő: szem, fül; Beavatkozó: kéz, láb, hangszál.
    *   *Robot:* Érzékelő: kamera, infra; Beavatkozó: motorok, karok.
    *   *Szoftverágens:* Érzékelő: billentyűleütés, hálózati csomag; Beavatkozó: képernyőre írás, fájlküldés [1].

### Racionális ágens
Olyan ágens, amely minden lehetséges észlelési sorozat esetén azt a cselekvést választja, amely a rendelkezésre álló ismeretek és észlelések alapján várhatóan maximalizálja a **teljesítménymértéket** (sikert) [3], [4].
*   **Ágensfüggvény ($f: P^* \to A$):** Az észlelési sorozatot képezi le cselekvésre [3], [4].
*   **Ágensprogram:** A függvény konkrét implementációja, amely a fizikai architektúrán fut [3], [2].

## 2. Feladatkörnyezet (PEAS modell)
Az ágens racionalitását a **PEAS** négyes határozza meg [5]:
1.  **P**erformance (Teljesítménymérték): A sikeresség kritériuma (pl. porszívónál a tisztaság).
2.  **E**nvironment (Környezet): Ahol az ágens működik.
3.  **A**ctuators (Beavatkozók): Amivel cselekszik.
4.  **S**ensors (Érzékelők): Amivel észlel.

### A környezet tulajdonságai
A környezetek különböző dimenziók mentén osztályozhatók [6]-[7], [8]-[9]:
*   **Teljesen vs. Részlegesen megfigyelhető:** Az ágens látja-e a teljes állapotot (pl. sakk vs. póker).
*   **Determinisztikus vs. Sztochasztikus:** A következő állapotot egyértelműen meghatározza-e a jelenlegi állapot és a cselekvés (pl. sakk vs. kockadobás).
*   **Epizódszerű vs. Sorozatszerű:** A döntések hatása átnyúlik-e a jövőbe (pl. osztályozás vs. sakk).
*   **Statikus vs. Dinamikus:** Változik-e a környezet, amíg az ágens gondolkodik.
*   **Diszkrét vs. Folytonos:** Véges vagy végtelen sok állapot/cselekvés lehetséges.
*   **Egyágenses vs. Többágenses:** Egyedül van-e vagy másokkal (kooperatív/versengő) interakcióban.

## 3. Ágenstípusok
Az ágensek belső működésük bonyolultsága szerint csoportosíthatók [10], [4]-[8]:
1.  **Egyszerű reflexszerű ágens:** Csak a pillanatnyi észlelést veszi figyelembe ("Ha piszkos, szívd fel"). Nincs memóriája.
2.  **Modellalapú ágens:** Belső állapotot (memóriát) tart fenn a világ nem látható részeinek követésére. Tudja, "hogyan működik a világ".
3.  **Célorientált ágens:** Céljai vannak (pl. "eljussak B-be"), és olyan cselekvéseket választ, amelyek közelebb visznek a célhoz (keresés, tervezés).
4.  **Hasznosságorientált ágens:** Nemcsak a célt akarja elérni, hanem "jól" (pl. gyorsan, olcsón). Hasznosságfüggvénnyel értékeli az állapotokat.
5.  **Tanuló ágens:** Képes a tapasztalatai alapján javítani a működését és tudását.

## 4. Ítéletkalkulus (Logika)
A logikai ágens tudásbázissal rendelkezik, és következtetéssel hoz döntéseket [9].

### Szintaxis és Szemantika
*   **Szintaxis:** A helyes formulák (mondatok) képzésének szabályai.
    *   *Elemei:* Ítéletváltozók ($P, Q$), logikai konstansok (Igaz, Hamis), kötőszavak ($\neg, \wedge, \vee, \rightarrow, \leftrightarrow$) [9].
*   **Szemantika:** A mondatok jelentése (igazságértéke) a lehetséges világokban (modellekben).
*   **Logikai következmény ($A \models B$):** $B$ logikai következménye $A$-nak, ha minden olyan modellben, ahol $A$ igaz, $B$ is igaz [9].

### Tételbizonyítási módszerek
Hogyan döntjük el, hogy egy állítás következik-e a tudásbázisból? [11]
1.  **Igazságtábla módszer:** Az összes lehetséges interpretáció (sor) végigpróbálása. (Teljes, de exponenciális idejű).
2.  **Quine-algoritmus:** Fa-struktúrájú kiértékelés, amely egyszerűsíti az igazságtáblát (pl. ha $P$ igaz, akkor $P \vee Q$ már biztosan igaz).
3.  **Formális levezetés (Dedukció):** Következtetési szabályok (pl. Modus Ponens: $A, A \to B \Rightarrow B$) alkalmazása a szintaxis szintjén.
4.  **Rezolúció:**
    *   Cél: Bizonyítani, hogy $KB \models \alpha$.
    *   Módszer: Indirekt bizonyítás. Tegyük fel, hogy $KB \wedge \neg \alpha$ (a tudásbázis és a következmény tagadása) kielégíthetetlen (ellentmondásra vezet).
    *   **Klóz formára** hozás (CNF): Minden mondatot $L_1 \vee \dots \vee L_k$ alakra hozunk.
    *   **Rezolúciós szabály:** Ha van $P \vee A$ és $\neg P \vee B$, akkor következik $A \vee B$ (a $P$ és $\neg P$ "kiütik" egymást) [12].

# 10. Tétel: Problémareprezentáció, Keresési algoritmusok és Kétszemélyes játékok

Ez a tétel az intelligens ágensek problémamegoldó képességeit tárgyalja: hogyan modellezhető egy probléma gráffal, hogyan találhatunk megoldást (keresés), és hogyan hozhatunk döntéseket versengő környezetben (játékok).

## 1. Problémareprezentáció (Állapottér)
A problémamegoldó ágens a megoldást (cselekvéssorozatot) kereséssel állítja elő egy állapottérben.
A probléma formális elemei [1], [2]:
*   **Állapotok halmaza (S):** Minden lehetséges szituáció (pl. sakkban a tábla állása).
*   **Kezdőállapot ($s_0$):** Ahonnan az ágens indul.
*   **Cselekvések (Operátorok):** Állapotátmenet-függvény, amely megadja, hogy egy állapotból milyen új állapotba juthatunk [3].
*   **Célteszt:** Eldönti egy állapotról, hogy célállapot-e.
*   **Útköltség:** A megoldáshoz vezető út "költsége" (pl. távolság, idő, lépésszám).
*   **Gráf reprezentáció:** Az állapotok a csúcsok, a cselekvések az élek [4].

## 2. Vak (Nem informált) keresések
Ezek az algoritmusok nem rendelkeznek információval arról, hogy a cél milyen "messze" van, csak a gráfot járják be szisztematikusan [5].

*   **Szélességi keresés (BFS):**
    *   Szintenként halad (először a szomszédokat nézi).
    *   **FIFO** (Sor) adatszerkezetet használ [6].
    *   **Tulajdonságai:** Teljes (megtalálja a megoldást, ha van), Optimális (ha minden lépés költsége 1), de nagy a memóriaigénye ($O(b^d)$) [7].
*   **Mélységi keresés (DFS):**
    *   Egy ágon megy ameddig tud, majd visszalép.
    *   **LIFO** (Verem) adatszerkezetet használ [8].
    *   **Tulajdonságai:** Kis memóriaigény ($O(b \cdot m)$), de nem optimális és végtelen ágakon eltévedhet (nem teljes) [8].
*   **Iteratívan mélyülő keresés (IDS):**
    *   Mélységi keresést végez növekvő mélységkorláttal.
    *   Egyesíti a BFS optimalitását és teljességét a DFS kis memóriaigényével [9].
*   **Egyenletes költségű keresés (UCS):**
    *   Mindig a legkisebb *eddigi* útköltségű ($g(n)$) csomópontot terjeszti ki. Optimális bármilyen pozitív költségnél [10].

## 3. Heurisztikus (Informált) keresések
Ezek az algoritmusok **heurisztikát** ($h(n)$) használnak, amely megbecsüli az adott állapottól a célig hátralévő költséget [11].
Kiértékelő függvény: $f(n) = g(n) + h(n)$ (eddigi út + becsült hátralévő).

*   **Mohó legjobbat először (Greedy Best-First):**
    *   Csak a heurisztikát nézi ($f(n) = h(n)$). Gyors, de nem optimális és nem teljes [12].
*   **A* (A-csillag) algoritmus:**
    *   Az eddigi és a becsült költséget is figyelembe veszi ($f(n) = g(n) + h(n)$) [13].
    *   **Optimalitás feltétele:** A heurisztika legyen **elfogadható** (admissible), azaz soha ne becsülje túl a tényleges költséget ($h(n) \le h^*(n)$) [14].

## 4. Lokális keresések
Nem a megoldáshoz vezető utat keresik, hanem a legjobb állapotot (pl. optimalizálás). Kis memóriaigényűek [15].

*   **Hegymászó módszer (Hill-Climbing):**
    *   Mindig a legjobb szomszéd irányába lép.
    *   **Hátránya:** Beragadhat lokális optimumba (nem a legmagasabb csúcs, de minden szomszédja rosszabb) [16].
*   **Szimulált lehűtés (Simulated Annealing):**
    *   Megenged "rosszabb" lépéseket is véletlenszerűen, hogy kimeneküljön a lokális optimumból. A valószínűség a "hőmérséklet" csökkenésével egyre kisebb [17].
*   **Genetikus algoritmusok:**
    *   Az evolúciót utánozza: populációt tart fenn, szelekciót, keresztezést és mutációt alkalmaz a jobb megoldások előállítására [18].

## 5. Kétszemélyes játékok
Teljes információjú, zérusösszegű játékok (pl. sakk), ahol a két fél (MAX és MIN) céljai ellentétesek [19].

*   **Minimax algoritmus:**
    *   A teljes játékfát (vagy egy részét) generálja. A leveleken hasznosságfüggvényt számol.
    *   Lentről felfelé: A **MAX** szinten a maximumot, a **MIN** szinten a minimumot választjuk (az ellenfél a legjobbat lépi ellenünk) [20].
*   **Alfa-Béta vágás (Pruning):**
    *   A Minimax optimalizálása. Nem vizsgálja meg azokat az ágakat, amelyekről már tudjuk, hogy nem befolyásolják a végeredményt (mert a másik fél úgysem engedné oda a játékot) [21], [22].
    *   **Vágási szabály:** Ha $\alpha \ge \beta$, akkor az adott ágat levágjuk (nem vizsgáljuk tovább) [23].

# 11. Tétel: A gépi tanulás fajtái, algoritmusai és neurális hálózatok

Ez a tétel a mesterséges intelligencia azon ágával foglalkozik, ahol a rendszerek nem explicit programozás, hanem adatok és tapasztalatok útján szereznek tudást,[1],[2].

## 1. A gépi tanulás alapfogalmai
A gépi tanulás (Machine Learning - ML) olyan rendszerek tervezése, amelyek tapasztalatokból (adatokból) tudást generálnak, hogy javítsák teljesítményüket jövőbeli feladatokban,[1],[3].
*   **Nehézsége:** Véges számú mintából kell tanulni, de végtelen számú esetben kell helyesen alkalmazni az elsajátított tudást,[1].
*   **Adatok előkészítése:** A tanuláshoz használt nyers adatokat tisztítani és transzformálni kell (zajszűrés, hiányzó adatok kezelése, jellemzőszelekció),[4],[5].

## 2. A tanulás fő típusai

### A) Felügyelt tanulás (Supervised Learning)
Rendelkezésre áll egy **tanító (tréning) adathalmaz**, ahol ismerjük a bemenetet és a hozzá tartozó helyes kimenetet (címkét) is,[6],[7].
Cél: Egy olyan modell (függvény) tanulása, amely új, ismeretlen adatokra is helyes kimenetet ad.
1.  **Osztályozás (Classification):** A kimenet diszkrét érték (osztálycímke),[8],[9].
    *   *Példák:* Spam szűrés (spam/nem spam), kézírás felismerés,[10].
    *   *Típusai:* Egyosztályos, Kétosztályos (bináris), Többosztályos,[9].
    *   **Döntési fák (Decision Trees):** A tanuló adatokból szabályokat (IF-THEN) generál fa struktúrában. A belső csomópontok tesztek az attribútumokon, a levelek az osztálycímkék. A fa építésekor a "legjobban szeparáló" attribútumot választjuk (pl. információnyereség alapján),[11],[12],[13].
    *   *Egyéb modellek:* Naív Bayes, k-legközelebbi szomszéd (k-NN), Support Vector Machine (SVM),[14].
2.  **Regresszió:** A kimenet folytonos érték,[15],[16].
    *   *Példák:* Ingatlanár becslése, hőmérséklet előrejelzése,[17].
    *   *Módszerek:* Lineáris regresszió (egyenes/hipersík illesztése), Polinomiális regresszió,[18].
3.  **Túltanulás (Overfitting):** A modell túlságosan a tréning adatokra illeszkedik (bemagolja a zajt is), ezért az új (teszt) adatokon rosszul teljesít. Megoldása: több adat, regularizáció, modell egyszerűsítése,[19],[20].

### B) Nem felügyelt tanulás (Unsupervised Learning)
Nincs címkézett tanító adatbázis, csak a bemeneti adatok állnak rendelkezésre. A cél az adatokban rejlő rejtett mintázatok, struktúrák feltárása,[20],[21].
1.  **Csoportosítás (Clustering):** Hasonló objektumok csoportba rendezése,[22].
    *   **k-means algoritmus:** Iteratív módszer. $k$ db középpontot (centroid) választunk, minden elemet a legközelebbihez rendelünk, majd újraszámoljuk a középpontokat. Addig ismételjük, amíg a csoportok nem változnak,[23],[24].
2.  **Asszociációs szabályok bányászata:** Gyakran együtt előforduló elemek feltárása (pl. bevásárlókosár-analízis: "Aki sört vesz, pelenkát is vesz"),[25],[26].

### C) Félig felügyelt tanulás (Semi-supervised Learning)
A felügyelt és nem felügyelt tanulás kombinációja. Kevés címkézett és sok címkézetlen adatot használ (pl. klaszterezéssel segít a címkézésben),[27],[28].

### D) Megerősítéses tanulás (Reinforcement Learning - RL)
A tanulás próba-szerencse alapon, a környezettel való interakció során történik. Az ágens döntéseket hoz, amire a környezet **jutalommal** (reward) vagy büntetéssel reagál,[2].
*   **Elemek:** Állapot ($s$), Cselekvés ($a$), Jutalom ($r$), Stratégia ($\pi$),[29].
*   **Cél:** A hosszú távú jutalom maximalizálása.
*   **Típusai:**
    *   *Passzív:* A stratégia rögzített, csak a hasznosságot tanulja.
    *   *Aktív:* A stratégiát is változtatja (felfedezés vs. kihasználás),[30].
*   **Algoritmusok:** Q-tanulás (Q-learning), SARSA,[31].

## 3. Mesterséges neurális hálózatok (ANN)
Az emberi agy működése által inspirált matematikai modell,[32].
*   **Felépítése:** Mesterséges neuronokból (csomópontokból) áll, amelyek rétegekbe rendeződnek.
*   **Működése:** A neuronok bemeneti jeleket fogadnak, azokat súlyozzák, összegezik, majd egy **aktivációs függvényen** (nemlinearitás) átvezetve kimenetet állítanak elő.
*   **Tanítás:** A hálózat súlyainak módosítása (pl. hiba-visszaterjesztés / backpropagation) a kimeneti hiba minimalizálása érdekében,[33].
*   **Mélytanulás (Deep Learning):** Sok rejtett réteggel rendelkező neurális hálók, amelyek képesek bonyolult mintázatok (pl. képek, beszéd) felismerésére,[33].

# 1. Tétel: Az információ reprezentációi (számrendszerek)

Ez a tétel a numerikus (egész, fix- és lebegőpontos) és nem numerikus adatok tárolási módjait, valamint a hibajavító kódolást tárgyalja.

## 1. Endianitás (Endianness)
A bájtsorrendet határozza meg, amikor egy adat több bájton tárolódik a memóriában.
*   **Little-Endian (LE):** A legkisebb helyiértékű bájt (LSB) kerül a legkisebb memóriacímre (pl. Intel, AMD processzorok). "Kicsi a végén" [1], [2].
*   **Big-Endian (BE):** A legnagyobb helyiértékű bájt (MSB) kerül a legkisebb memóriacímre (pl. hálózati protokollok, PowerPC). "Nagy a végén" [3], [2].

## 2. Egész számok ábrázolása (Integer)
Bináris számrendszert használ. $n$ biten $2^n$ érték ábrázolható.
*   **Előjel nélküli (Unsigned):** Csak pozitív számok. Tartomány: $0 \dots 2^n - 1$ [4].
*   **Előjeles (Signed):**
    *   **1-es komplemens:** A biteket invertáljuk (0$\to$1, 1$\to$0). Hátránya: két nulla van (+0, -0) [4].
    *   **2-es komplemens:** Az 1-es komplemenshez hozzáadunk 1-et.
        *   Előnye: egyetlen nulla van, a kivonás visszavezethető összeadásra.
        *   Tartomány: $-2^{n-1} \dots 2^{n-1}-1$ [5], [6].

## 3. Valós számok ábrázolása

### Fixpontos (Fixed-point)
A tizedespont (kettőspont) helye rögzített a bitsorozaton belül.
*   **Jellemzők:**
    *   **$p$**: A tizedesjegyeket reprezentáló bitek száma.
    *   **$\Delta r$ (Differencia):** A számrendszer finomsága (legkisebb lépésköz), $\Delta r = 2^{-p}$ [7], [8].
*   **Előny:** Egyszerű aritmetika (mint az egészeknél).
*   **Hátrány:** Korlátozott értéktartomány és pontosság.

### Lebegőpontos (Floating-point)
A tizedespont helye "lebeg", így nagyon nagy és nagyon kis számok is ábrázolhatók (normálalak).
*   **Képlet:** $(-1)^S \cdot M \cdot R^E$, ahol $S$ az előjel, $M$ a mantissza, $R$ az alap, $E$ a kitevő.
*   **IEEE-754 Szabvány (32 bites "single" pontosság):**
    *   **Felépítés:** 1 bit előjel ($S$), 8 bit exponens ($E$, feszített/excess kódolással), 23 bit mantissza ($M$).
    *   **Normalizálás:** A mantissza mindig $1.xxxx$ alakú (a vezető 1-est nem tárolják, ez a "rejtett bit") [9], [10].
    *   **Speciális értékek:** $\pm 0$, $\pm \infty$ (végtelen), NaN (Not a Number - pl. 0/0) [11].
*   **Egyéb rendszerek:** DEC-32, IBM-32 (eltérő alap vagy kódolás) [12].

## 4. Nem numerikus információk
Szöveges információk kódolása karaktertáblákkal történik.
*   **ASCII:** Eredetileg 7 bites (128 karakter), az angol ábécére tervezve. Kiterjesztett változata 8 bites [13].
*   **BCD (Binary Coded Decimal):** 6 bites kódolás számok és betűk ábrázolására [14].
*   **Unicode (UTF-8):** Változó hosszúságú (8-32 bit) kódolás, amely a világ szinte összes írásjelét támogatja [13].

## 5. Hibadetektálás és javítás
Célja az adatátvitel során keletkező hibák észlelése és javítása redundancia (többletinformáció) hozzáadásával.
*   **Paritásbit:** A legegyszerűbb módszer. Egy extra bitet adunk az adathoz, hogy az 1-esek száma páros (vagy páratlan) legyen. Csak a hiba tényét jelzi (páratlan számú hiba esetén), javítani nem tud [15].
*   **Hamming-kód:** Képes **1 bites hiba javítására** és 2 bites hiba jelzésére. Több paritásbitet használ speciális pozíciókban (a 2 hatványainál), amelyek az adatbitek különböző kombinációit ellenőrzik [13].

# 2. Tétel: Az ALU felépítése és működése

Ez a tétel a processzor számítási központját, az ALU-t (Arithmetic Logic Unit), valamint az alapvető aritmetikai műveletek (összeadás, kivonás, szorzás, osztás) digitális áramköri megvalósítását tárgyalja.

## 1. Az ALU felépítése és az Univerzális teljesség
Az ALU a CPU azon része, amely az aritmetikai és logikai utasításokat hajtja végre.
*   **Felépítése:**
    *   **Bemenetek:** Két operandus ($A$, $B$), vezérlőjelek (műveletkód), és esetleges státusz bitek (pl. Carry In).
    *   **Kimenetek:** Eredmény ($F$) és státusz bitek (Flags: Zero, Carry, Overflow, Sign).
    *   **Működése:** A vezérlőjelek egy multiplexeren keresztül választják ki, hogy melyik belső egység (aritmetikai vagy logikai) eredménye kerüljön a kimenetre [1], [2].
*   **Univerzális teljesség elve:** Bármely logikai függvény (és így bármely aritmetikai művelet) megvalósítható kizárólag **NAND** vagy kizárólag **NOR** kapuk segítségével. A mai processzorok (CMOS technológia) jellemzően ezekre épülnek [3].

## 2. Összeadó áramkörök
A bináris összeadás az ALU legalapvetőbb művelete.

*   **Fél-összeadó (Half Adder - HA):** Két 1 bites számot ad össze.
    *   Kimenetek: Összeg ($S = A \oplus B$) és Átvitel ($C_{out} = A \cdot B$).
    *   Hátránya: Nem kezeli az előző helyiértékről jövő átvitelt ($C_{in}$) [2], [4].
*   **Teljes összeadó (Full Adder - FA):** Két 1 bites számot és egy bejövő átvitelt ($C_{in}$) ad össze.
    *   Két fél-összeadóból épül fel.
    *   $S = A \oplus B \oplus C_{in}$ [4], [5].
*   **Soros átvitelű összeadó (Ripple Carry Adder - RCA):** Többbites összeadáshoz a Teljes Összeadókat láncba kötjük.
    *   Lassú, mert az átvitelnek ($C_{out}$) végig kell „csorognia” az összes biten a legkisebbtől a legnagyobbig (LSB $\to$ MSB). Időigény: $\approx 2n$ kapukésleltetés [5], [6].
*   **Átvitelgyorsító összeadó (Look-Ahead Carry Adder - LACA):**
    *   Párhuzamosan számolja ki az átvitel biteket, nem várja meg az előző fokozatokat. Bonyolultabb áramkör, de sokkal gyorsabb [7], [8].

## 3. Kivonó áramkörök
A kivonás kétféleképpen valósítható meg:
1.  **Teljes kivonóval (Full Subtractor):** Hasonló a teljes összeadóhoz, de „kölcsön” (Borrow) bemenete és kimenete van [8], [9].
2.  **Összeadóval (2-es komplemens):** A gyakorlatban ezt használják. A kivonást visszavezetik összeadásra: $A - B = A + (-B)$.
    *   A $B$ operandus bitjeit invertálják, és a $C_{in}$ bemenetre 1-et adnak (ez állítja elő a 2-es komplemenst) [10].

## 4. Szorzás (Hagyományos módszer)
A bináris szorzás az „papíron végzett” módszerhez hasonlóan visszavezethető **eltolásokra (shift)** és **összeadásokra (add)**.
*   **Shift & Add algoritmus:**
    *   Ha a szorzó aktuális bitje 1, a szorzandót hozzáadjuk a részeredményhez.
    *   Ezután a szorzandót balra léptetjük (vagy a részeredményt jobbra).
    *   $N$ bites számok szorzásához $N$ lépés szükséges. Az eredmény $2N$ bites lehet [11], [12], [13].

## 5. Osztás (Hagyományos módszer)
Az osztás a kivonások és eltolások sorozata (a „papíron végzett” osztás gépesítése).
*   **Hagyományos iteratív osztás:**
    *   Az osztót próbáljuk kivonni a maradékból (kezdetben az osztandóból).
    *   Ha az eredmény pozitív, a hányados aktuális bitje 1, és a kivonás érvényes.
    *   Ha negatív, a bit 0, és visszaállítjuk az eredeti értéket (vagy nem végezzük el a kivonást).
    *   Ezután shifteljük az osztót vagy a maradékot. Ez egy lassú folyamat [14], [15].

# 3. Tétel: Vezérlő egységek (huzalozott és mikrokódos)

Ez a tétel a CPU „agyát”, a vezérlő egységet tárgyalja, amely értelmezi az utasításokat és irányítja az adatutakat a processzorban.

## 1. A vezérlő egység (CU) feladata
A vezérlő egység (Control Unit) feladata a memóriából érkező gépi kódú utasítások **értelmezése** (dekódolása), részműveletekre bontása, és a megfelelő **vezérlőjelek** (control signals) előállítása a megfelelő sorrendben a többi egység (ALU, regiszterek, memória) számára [1][2].

Tervezése két alapvető módon történhet:
1.  **Huzalozott (Hardwired):** Fix logikai áramkörökkel.
2.  **Mikroprogramozott (Microprogrammed):** Programozható logikai elemekkel vagy memóriával [3].

## 2. Huzalozott vezérlők (Hardwired)
Kombinációs és sorrendi (szekvenciális) logikai hálózatokból épülnek fel. A vezérlést fix áramkörök valósítják meg.
*   **Jellemzői:** Nagyon gyors működés, de nehézkes a módosítása (újra kell tervezni a hardvert). Jellemzően **RISC** (Reduced Instruction Set Computing) architektúráknál használják, ahol egyszerűbbek az utasítások [4].
*   **Modellezése:** Állapotgépekkel (FSM - Finite State Machine) történik:
    *   **Mealy-modell:** A kimenet (vezérlőjelek) a rendszer pillanatnyi állapotától **és** a bemeneti jelektől is függ. Gyorsabb reagálású, de aszinkron zavarokra érzékenyebb [5].
    *   **Moore-modell:** A kimenet **kizárólag** a rendszer pillanatnyi állapotától függ. Stabilabb, szinkron működésű [6].

## 3. Mikroprogramozott vezérlők
A vezérlő logika egy gyors memóriában (ROM/PLA) tárolt „program” (mikrokód) formájában valósul meg.
*   **Működése:** A gépi kódú utasításokat egy köztes kód (mikrokód) segítségével képezi le hardveres vezérlőjelekre. Egy gépi utasítás végrehajtása egy **mikroprogram** lefuttatását jelenti [7][8].
*   **Jellemzői:** Rugalmas (könnyen javítható/bővíthető a firmware frissítésével), de lassabb a memóriahozzáférés miatt. Jellemzően **CISC** (Complex Instruction Set Computing) rendszerekben használják [9].
*   **Felépítése:** *Mikroutasítás regiszter*, *Vezérlő memória* (Control Memory), *Címgenerátor* [8].

### Típusai (a mikrokód szélessége szerint):
1.  **Horizontális (Vízszintes):**
    *   Minden vezérlőjelhez külön bit tartozik a mikroutasításban.
    *   **Előny:** Gyors, nagymértékű párhuzamosítást tesz lehetővé (több egység egyszerre vezérelhető).
    *   **Hátrány:** Nagyon széles a mikrokód, sok memóriát igényel [10][11].
2.  **Vertikális (Függőleges):**
    *   A vezérlőjeleket kódoltan tárolják (pl. $n$ vezérlőjelhez $\log_2 n$ bit). Dekódoló áramkör szükséges a kimeneten.
    *   **Előny:** Takarékos a memóriával (rövidebb utasítások).
    *   **Hátrány:** Lassabb a dekódolás miatt, és korlátozottabb a párhuzamosítás [12][13].

# 4. Tétel: Folyamatok kezelése multiprogramozott rendszerekben

Ez a tétel a futó programok (folyamatok) absztrakcióját, az operációs rendszer általi ütemezésüket és az egymással való együttműködésük (szinkronizáció) eszközeit tárgyalja.

## 1. A folyamat (Process) fogalma
A folyamat egy **végrehajtás alatt álló program**,.
*   **Multiprogramozás:** Több folyamat van a memóriában, és a CPU váltogat közöttük (konkurens futás), hogy növelje a kihasználtságot,.
*   **Állapotai:**
    *   **Fut (Running):** A CPU éppen ezt a folyamatot hajtja végre (CPU-nként csak egy lehet),.
    *   **Futásra kész (Ready):** A folyamat kész a futásra, minden erőforrása megvan, csak a CPU-ra vár,.
    *   **Várakozik/Blokkolt (Waiting):** Valamilyen eseményre (pl. I/O befejezésére) vár, addig nem kaphat CPU-t,.
*   **Folyamatleíró blokk (PCB):** Az OS ebben az adatszerkezetben tárolja a folyamat adatait (állapot, regiszterek, programszámláló, prioritás),.
*   **Környezetváltás (Context Switch):** Amikor az OS elveszi a CPU-t egy folyamattól, elmenti az állapotát a PCB-be, és betölti a következő folyamat állapotát. Ez adminisztrációs időveszteséggel jár,.

## 2. Ütemezés (Scheduling)
Az ütemező dönti el, melyik folyamat kapja meg a CPU-t és mennyi időre.
*   **Szintjei:**
    *   *Rövidtávú (Short-term):* Melyik *futásra kész* folyamat kapja a CPU-t (nagyon gyakori döntés),.
    *   *Középtávú:* Swap-elés (ki/be mozgatás a memória és a lemez között) a terhelés csökkentésére,.
    *   *Hosszútávú:* Melyik új munka kerülhet be a rendszerbe (batch rendszereknél),.
*   **Típusai:**
    *   *Nem preemptív:* A folyamat addig fut, amíg önszántából le nem mond a CPU-ról (pl. várakozik vagy kilép),.
    *   *Preemptív:* Az OS megszakíthatja a futó folyamatot (pl. lejárt az időszelet) és elveheti tőle a CPU-t,.

### Ütemezési algoritmusok
1.  **FCFS (First Come, First Served):** Érkezési sorrendben. Nem preemptív. Hátránya a *konvoj-hatás* (egy hosszú folyamat feltartja a rövideket),.
2.  **SJF (Shortest Job First):** A legrövidebb löketidejű folyamat jön. Optimális átlagos várakozási időt ad, de a löketidőt nehéz becsülni,.
3.  **Round Robin (RR - Körforgó):** Mindenki kap egy fix időszeletet (time quantum). Ha lejár, a folyamat a sor végére kerül. Preemptív, idősztásos rendszerekhez ideális,.
4.  **Prioritásos:** A fontosság alapján dönt. Probléma a *kiéheztetés* (alacsony prioritású sosem fut), megoldása az *öregítés* (aging),.

## 3. Szinkronizáció
Ha a folyamatok közös erőforrást (pl. változót) használnak, összehangolásra van szükség.
*   **Versenyhelyzet (Race Condition):** A végeredmény attól függ, milyen sorrendben futnak le a folyamatok utasításai. Ez hibás működéshez vezethet,.
*   **Kritikus szakasz (Critical Section):** A program azon része, ahol közös erőforrást ér el. Egyszerre csak egy folyamat tartózkodhat a kritikus szakaszában (kölcsönös kizárás),,.

### Megoldási módszerek
1.  **Szemafor (Semaphore):**
    *   Egy egész típusú változó, két atomi művelettel: *P (wait)* és *V (signal)*,.
    *   A belépéskor a folyamat csökkenti az értékét (ha 0, akkor várakozik), kilépéskor növeli (és felébreszt egy várakozót).
2.  **Mutex (Mutual Exclusion):** Bináris szemafor, amely csak zárolt/nyitott állapotban lehet,.
3.  **Monitor:** Magas szintű nyelvi szerkezet, amely automatikusan biztosítja, hogy egyszerre csak egy folyamat legyen aktív benne,.

# 5. Tétel: A holtpont (Deadlock) fogalma és kezelése

Ez a tétel a holtpont jelenségét, kialakulásának szükséges feltételeit és a lehetséges védekezési stratégiákat tárgyalja.

## 1. A holtpont fogalma
Holtpontról akkor beszélünk, ha folyamatok egy halmazában minden folyamat olyan eseményre (általában erőforrás felszabadulására) vár, amelyet csak egy másik, ugyancsak ebben a halmazban lévő (várakozó) folyamat tudna előidézni [1].
*   **Példa:** Két folyamatnak szüksége van A és B erőforrásra. Az egyik lefoglalta A-t és vár B-re, a másik lefoglalta B-t és vár A-ra [2].

## 2. A kialakulás szükséges feltételei
A holtpont akkor és csak akkor jöhet létre, ha az alábbi négy feltétel **egyszerre** teljesül [3]:
1.  **Kölcsönös kizárás (Mutual Exclusion):** Az erőforrásokat egyszerre csak egy folyamat használhatja (pl. nyomtató).
2.  **Foglalva várakozás (Hold and Wait):** Van olyan folyamat, amely már birtokol erőforrást, miközben egy másikra várakozik.
3.  **Nem elvehető erőforrások (No Preemption):** Az erőforrást a folyamattól nem lehet erőszakkal elvenni, csak ő maga szabadíthatja fel.
4.  **Körkörös várakozás (Circular Wait):** A folyamatok egymásra várnak egy zárt láncban (P1 vár P2-re, P2 vár ... Pn-re, Pn vár P1-re).

## 3. Holtpontkezelési stratégiák

### A) A probléma figyelmen kívül hagyása (Strucc algoritmus)
Úgy teszünk, mintha a probléma nem létezne. Ritkán előforduló holtpontoknál, nem kritikus rendszerekben alkalmazható (pl. újraindítjuk a gépet), mert a megelőzés költsége túl nagy lenne [4].

### B) Megelőzés (Prevention)
A négy szükséges feltétel közül legalább az egyiket **kizárjuk**, így lehetetlenné tesszük a holtpontot [5].
*   *Foglalva várakozás kizárása:* A folyamatnak induláskor egyszerre kell kérnie minden erőforrást [6]. (Hátrány: rossz erőforrás-kihasználás, éhezés).
*   *Körkörös várakozás kizárása:* Az erőforrásokat sorszámozzuk, és csak növekvő sorrendben lehet őket igényelni [7].

### C) Elkerülés (Avoidance)
A rendszer futás közben, minden erőforráskérésnél mérlegeli, hogy a kérés teljesítése biztonságos-e.
*   **Biztonságos állapot:** Létezik a folyamatoknak olyan végrehajtási sorrendje (biztonságos sorozat), amellyel mindenki be tudja fejezni a futását [8].
*   **Bankár algoritmus (Dijkstra):** Ismerni kell hozzá minden folyamat *maximális* erőforrásigényét. Ha egy kérés teljesítése nem biztonságos állapotba vinné a rendszert (nem garantálható a befejezés), a kérést elutasítja vagy várakoztatja [9], [10].

### D) Detektálás és Helyreállítás (Detection & Recovery)
Megengedjük a holtpont kialakulását, de időközönként ellenőrizzük a rendszert.
*   **Detektálás:** Erőforrás-allokációs gráffal vagy várakozási gráffal keressük a köröket [11].
*   **Helyreállítás:**
    *   *Folyamat megszüntetése:* Minden érintett folyamat kilövése, vagy egyesével, amíg a kör megszűnik [12].
    *   *Erőforrás elvétele (Preemption):* Erőforrás erőszakos elvétele és a folyamat visszagörgetése (rollback) egy korábbi állapotba [13].

    