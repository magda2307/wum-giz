
# Grafy i Zastosowania – Notatki do najniższej oceny

## Definicje podstawowe grafów

**Graf nieskierowany** to uporządkowana para zbiorów $G = (V, E)$, gdzie $V$ to skończony zbiór **wierzchołków**, a $E$ – zbiór **krawędzi**. Każda krawędź $e = \{v,w\}$ jest **nieuporządkowaną** parą różnych wierzchołków z $V$. Mówimy, że taka krawędź **łączy** wierzchołki $v$ i $w$; wtedy $v$ i $w$ są **sąsiednie**, a krawędź $e$ jest z nimi **incydentna**. Graf nieskierowany reprezentuje z definicji relację symetryczną na zbiorze wierzchołków.

**Graf skierowany (digraf)** to para $G = (V, E)$, gdzie $V$ to zbiór wierzchołków, a $E$ jest zbiorem **skierowanych krawędzi**. Każda taka krawędź $e = (v, w)$ jest **uporządkowaną** parą wierzchołków z $V$. Mówimy, że krawędź $e$ **biegnie** od $v$ do $w$ (tj. **wychodzi** z $v$ i **wchodzi** do $w$). Krawędzie skierowane nazywamy także **łukami**. Graf skierowany odpowiada dowolnej relacji binarnej (niesymetrycznej) na zbiorze wierzchołków.

**Graf prosty** to graf (skierowany lub nieskierowany), który **nie posiada pętli ani krawędzi wielokrotnych**. *Pętla* to krawędź łącząca wierzchołek z samym sobą (postaći $(v,v)$). W grafie prostym żadne dwa wierzchołki nie są połączone więcej niż jedną krawędzią. Uwaga: w grafie **skierowanym** krawędzie $(v,w)$ i $(w,v)$ są traktowane jako różne – mogą wystąpić obie na raz i nie są uznawane za krawędź wielokrotną. *(Niniejszy kurs dotyczy głównie grafów prostych.)*

**Multigraf** to uogólnienie grafu prostego, w którym **dopuszczalne są krawędzie wielokrotne** łączące tę samą parę wierzchołków. **Hipergraf** to kolejna generalizacja grafu – jego **hiperkrawędzie** mogą łączyć jednocześnie więcej niż dwa wierzchołki (np. trojki, czwórki) i reprezentować relacje wyższej arności niż 2.

> **Przykład:** Graf pełny $K_5$ (5 wierzchołków, każdy z każdym) jest grafem prostym nieskierowanym. Gdybyśmy dodali kolejną krawędź między dowolną istniejącą parą wierzchołków $K_5$, otrzymalibyśmy multigraf. Z kolei hipergrafem byłaby struktura, w której np. jedna “krawędź” łączy jednocześnie wszystkie 5 wierzchołków.

## Stopnie wierzchołków i ich własności

**Stopień wierzchołka** $deg(v)$ w grafie nieskierowanym to liczba krawędzi incydentnych z tym wierzchołkiem. W grafie **prostym** pętla nie występuje, natomiast w grafach niespełniających tej własności przyjmuje się konwencję, że każda pętla $(v,v)$ *dodaje 2* do stopnia wierzchołka $v$. Wierzchołek o stopniu 0 nazywamy **izolowanym** (nie jest połączony z żadnym innym). Najmniejszy i największy stopień wierzchołka w grafie $G$ oznaczamy przez $\delta(G)$ oraz $\Delta(G)$, odpowiednio.

**Graf regularny** to graf, w którym wszystkie wierzchołki mają jednakowy stopień. Jeśli każdy wierzchołek ma stopień $r$, graf jest **$r$-regularny**. Przykładowo, graf 3-regularny określa się jako **graf kubiczny**. Grafy regularne mogą być zarówno skierowane, jak i nieskierowane (w digrafach regularność definiuje się osobno dla stopni wejściowych i wyjściowych).

*Własności:* W każdym grafie sumaryczna liczba **końców krawędzi** (incydencji) jest równa sumie stopni wszystkich wierzchołków. Zatem zachodzi **lemat o uściskach dłoni:** *suma stopni wszystkich wierzchołków grafu nieskierowanego jest liczbą parzystą* (dokładniej, jest równa dwa razy liczbie krawędzi). W konsekwencji liczba wierzchołków o stopniu nieparzystym w dowolnym grafie musi być parzysta (mogą to być np. 0, 2, 4,... wierzchołki).

W **grafie skierowanym** definiuje się osobno **stopień wejściowy** $indeg(v)$ (liczba łuków kończących się w $v$) oraz **stopień wyjściowy** $outdeg(v)$ (liczba łuków wychodzących z $v$). Dla każdego digrafu suma stopni wejściowych wszystkich wierzchołków jest równa sumie stopni wyjściowych (obie sumy równe są liczbie wszystkich krawędzi skierowanych).

## Izomorfizm grafów

Grafy $G\_1=(V\_1, E\_1)$ oraz $G\_2=(V\_2, E\_2)$ nazywamy **izomorficznymi**, jeśli istnieje odwzorowanie bijektywne $f: V\_1 \to V\_2$ takie, że dla każdych dwóch wierzchołków $v, w \in V\_1$ zachodzi: $v$ i $w$ są połączone krawędzią w $G\_1$ wtedy i tylko wtedy, gdy $f(v)$ i $f(w)$ są połączone krawędzią w $G\_2$. Intuicyjnie oznacza to, że grafy te mają identyczną strukturę po odpowiednim “przemianowaniu” wierzchołków. Izomorfizm grafów zachowuje wszystkie własności związane z połączeniami (stopnie wierzchołków, sąsiedztwa itp.).
* Czy liczba wierzchołków w obu grafach jest taka sama? Tak, oba grafy mają 4 wierzchołki.
* Czy liczba krawędzi w obu grafach jest taka sama? Tak, oba grafy mają 4 krawędzie.
* Czy sekwencja stopni w obu grafach jest taka sama? Tak, każdy wierzchołek jest stopnia 2.
* Jeśli wierzchołki w jednym grafie mogą utworzyć cykl o długości k, czy możemy znaleźć tę samą długość cyklu w drugim grafie? Tak, każdy graf ma cykl o długości 4.
* A jeśli możemy odpowiedzieć twierdząco na wszystkie cztery powyższe pytania, to wykresy są izomorficzne. Innymi słowy, są to równoważne wykresy, tylko w różnych formach.
> **Zastosowania:** Rozpoznawanie izomorfizmu grafów ma znaczenie m.in. w chemii (porównywanie struktur cząsteczek), przy wyszukiwaniu patentów czy porównywaniu schematów sieci. **Uwaga:** Nie jest znany efektywny, wielomianowy algorytm stwierdzania izomorficzności dwóch dowolnych grafów – problem ten leży w klasie NP i wciąż nie wiadomo, czy jest NP-zupełny. Mimo to praktycznie, dla wielu klas grafów istnieją sprawne metody porównywania.

## Ważne rodzaje grafów

Poniżej zebrano podstawowe rodziny grafów wraz z ich oznaczeniami i charakterystykami (zakładamy grafy proste, bez pętli, jeśli nie zaznaczono inaczej):

* **Graf zerowy** – graf, w którym zbiory wierzchołków i krawędzi są puste. (Czasem termin “graf zerowy” odnosi się też do grafu z pustym $E$, ale niepustym $V$ – wówczas graf taki częściej nazywa się grafem pustym.)

* **Graf pusty** $N\_n$ – graf na $n$ wierzchołkach bez żadnej krawędzi (czyli $E = \emptyset$). Ma $n$ wierzchołków i 0 krawędzi.

* **Graf pełny (kompletny)** $K\_n$ – graf na $n$ wierzchołkach, w którym każda możliwa krawędź między dwiema różnymi etykietami *istnieje*. Taki graf ma maksymalną liczbę krawędzi: $\frac{n(n-1)}{2}$ dla nieskierowanego (po jednej krawędzi między każdą parą). W wersji skierowanej kompletny digraf ma $n(n-1)$ łuków (po dwa w każdej nieuporządkowanej parze wierzchołków).

* **Graf dwudzielny** – graf, którego zbiór wierzchołków można rozbić na dwa rozłączne podzbiory $V\_1$ i $V\_2$ tak, że **każda** krawędź łączy wierzchołek z $V\_1$ z wierzchołkiem z $V\_2$ (nie ma krawędzi wewnątrz $V\_1$ ani wewnątrz $V\_2$). Notacja: $G=(V\_1, V\_2, E)$. Jeśli dodatkowo w grafie dwudzielnym występują *wszystkie możliwe* krawędzie między $V\_1$ a $V\_2$, jest to **graf pełny dwudzielny** ozn. $K\_{m,n}$ (dla $|V\_1|=m$, $|V\_2|=n$). Graf $K\_{m,n}$ ma $m+n$ wierzchołków i $m \cdot n$ krawędzi.

* **Ścieżka** $P\_n$ – graf utworzony przez ciąg $n$ wierzchołków połączonych kolejno krawędziami w ciąg linearny (tj. $v\_1$–$v\_2$–...–$v\_n$). Ścieżka na $n$ wierzchołkach zawiera dokładnie $n-1$ krawędzi. **Cykl** $C\_n$ – graf utworzony przez zamknięcie ścieżki, tj. $n$-wierzchołkowy cykl (np. $v\_1$–$v\_2$–...–$v\_n$–$v\_1$). Cykl $C\_n$ ma $n$ wierzchołków i $n$ krawędzi. Szczególnymi przypadkami są $P\_1$ (pojedynczy wierzchołek) i $C\_3$ (trójkąt).

* **Graf kołowy (wheel)** $W\_n$ – graf otrzymany przez dodanie nowego wierzchołka do grafu $C\_{n}$ i połączenie go krawędziami ze wszystkimi wierzchołkami tego $C\_n$. Taki graf $W\_n$ ma $n+1$ wierzchołków (cykl $C\_n$ plus tzw. *centrum* koła) oraz $2n$ krawędzi (n krawędzi cyklu + n krawędzi do centrum).

* **Hiperkostka** $Q\_i$ – graf o $2^i$ wierzchołkach, z których każdy można przedstawić jako binarny wektor długości $i$. Dwa wierzchołki są połączone krawędzią wtedy, gdy odpowiadające im $i$-bitowe ciągi różnią się dokładnie na jednej pozycji (czyli mają Hammingowską odległość 1). Przykładowo $Q\_3$ to *sześcian*: 8 wierzchołków odpowiada 8 różnym trójkom bitów, a krawędzie łączą każdy wierzchołek z trzema innymi (graf 3-regularny).

* **Graf drabinkowy** $LD\_i$ – graf utworzony jako iloczyn kartezjański $P\_i \times P\_2$. Intuicyjnie jest to “drabina” o $i$ szczeblach: dwa równoległe ciągi $P\_i$ (boki drabiny) połączone $i$ krawędziami poprzecznymi (szczeblami). Graf $LD\_i$ ma $2i$ wierzchołków oraz $3(i-1) + 2 = 3i - 2$ krawędzi (bo każdy z $i$ szczebli dodaje 1 krawędź do dwóch krawędzi obecnych między sąsiednimi szczeblami).

* **Grafy platońskie** – to grafy reprezentujące krawędzie i wierzchołki pięciu brył platońskich (np. czworościanu – $K\_4$, sześcianu, ośmiościanu, dwunastościanu i dwudziestościanu foremnego). Są to grafy 3-regularne lub 4-regularne i planarne (można je narysować bez przecięć na płaszczyźnie). Nie są one osobną rodziną w sensie parametrycznym, ale warto znać ich przykłady jako regularnych, symetrycznych grafów.

* **Graf Petersena** – słynny 3-regularny graf na 10 wierzchołkach i 15 krawędziach. Nie jest planarny i ma wiele ciekawych własności (np. brak cyklu Hamiltona). Często służy jako kontrprzykład w teorii grafów. Stanowi przykład grafu regularnego, który nie jest dwudzielny ani planarny.

## Ścieżki i cykle w grafach

**Ścieżka (droga)** w grafie to sekwencja wierzchołków $(v\_0, v\_1, ..., v\_k)$ taka, że każdy kolejny wierzchołek jest połączony krawędzią z poprzednim. Formalnie, istnieje ciąg krawędzi $(e\_1, e\_2, ..., e\_k)$, gdzie $e\_i = {v\_{i-1}, v\_i}$ dla $i=1,...,k$. Ścieżkę można także określić jako **naprzemienny ciąg wierzchołków i krawędzi** rozpoczynający i kończący się wierzchołkiem: $v\_0, e\_1, v\_1, e\_2, ..., e\_k, v\_k$, gdzie każde $e\_i$ łączy $v\_{i-1}$ z $v\_i$. Długością ścieżki nazywamy liczbę występujących w niej krawędzi (przyjmujemy, że ścieżka długości 0 to pojedynczy wierzchołek bez krawędzi).

Ścieżka **prosta** (prosty łańcuch) to taka, w której *żadna krawędź nie powtarza się*. Często przyjmuje się dodatkowo, że w ścieżce prostej nie powtarzają się również wierzchołki (poza ewentualnie początkowym i końcowym w cyklu) – taka ścieżka jest wówczas nazywana **elementarną**. (Różne źródła różnie definiują te pojęcia, dlatego należy zwracać uwagę na kontekst definicji.)

**Cykl** to zamknięta ścieżka – ścieżka, w której $v\_0 = v\_k$ (czyli początek i koniec to ten sam wierzchołek), oraz która ma co najmniej 3 krawędzie. Analogicznie jak wyżej, **cykl prosty** nie powtarza krawędzi, a **cykl elementarny** – nie powtarza żadnego wierzchołka poza początkowo-końcowym. **Obwód** grafu to długość najkrótszego cyklu w grafie (jeśli graf nie zawiera żadnego cyklu, mówimy że obwód jest nieskończony).

## Spójność grafu
Graf niepusty nazywamy **spójnym**, jeśli każde dwa jego różne wierzchołki można połączyć pewną ścieżką. Równoważnie: graf jest spójny, jeśli nie da się jego wierzchołków podzielić na dwa niepuste zbiory tak, by *brakowało* krawędzi między tymi dwoma częściami (tzn. graf nie jest sumą dwóch niepołączonych grafów). 
**Składowa spójna** to maksymalny (największy) podgraf spójny grafu – innymi słowy, spójna “część” grafu zawierająca pewien podzbiór wierzchołków. Każdy graf można jednoznacznie rozłożyć na swoje składowe spójne; liczbę składowych spójnych oznaczamy $c(G)$. Graf spójny ma $c(G)=1$. Graf całkowicie niespójny (pusty) na $n$ wierzchołkach ma $c(G)=n$.

W przypadku **grafów skierowanych** rozróżniamy spójność *słabą* i *silną*.

Graf **silnie spójny** (silnie spójny skierowany) to taki digraf, w którym dla każdej uporządkowanej pary **różnych** wierzchołków $u, v$ istnieje ścieżka *skierowana* od $u$ do $v$. Innymi słowy, z każdego wierzchołka da się dosć do każdego innego, *uwzględniając kierunki łuków*. 

Graf **słabo spójny** to graf skierowany, który jest spójny jeśli **pominąć kierunki** krawędzi, czyli zastąpić wszystkie łuki krawędziami nieskierowanymi – wtedy powstały graf nieskierowany jest spójny. Silna spójność pociąga za sobą słabą (graf silnie spójny jest oczywiście spójny po “zapomnieniu” kierunków), ale nie odwrotnie. 

**Składowe silnie spójne** i **składowe słabo spójne** definiuje się analogicznie jak w przypadku grafów nieskierowanych (maksymalne podgrafy silnie, względnie słabo spójne).

**Most** (lub **krawędź artykulacji**, **krawędź rozspajająca**) to krawędź, której usunięcie zwiększa liczbę składowych spójnych grafu. Innymi słowy, jest to krawędź, której usunięcie rozłącza graf – stanowi ona jedyne połączenie między dwoma fragmentami grafu.

**Punkt artykulacji** (czyli **wierzchołek rozdzielający**) to wierzchołek, którego usunięcie (wraz z wszystkimi incydentnymi z nim krawędziami) zwiększa liczbę składowych grafu. Inaczej: wierzchołek, po którego usunięciu graf się rozpada – ten wierzchołek “spinał” dwie lub więcej części sieci. Pojęcie to dotyczy tylko grafów nieskierowanych (w digrafach analogiem jest *punkt artykulacji silnej spójności*, rzadziej rozważany).

**Spójność krawędziowa** grafu spójnego $G$ to najmniejsza liczba krawędzi, jaką należy usunąć, aby graf stał się niespójny (lub równoważnie: aby liczba składowych wzrosła). Tę liczbę oznacza się $\lambda(G)$. Formalnie, $\lambda(G)$ to liczność najmniejszego *zbioru rozspajającego* (zbioru krawędzi, którego usunięcie rozspaja graf). Jeśli $\lambda(G) \ge k$, mówimy że graf jest **$k$-spójny krawędziowo**. Przykładowo, graf cykliczny $C\_4$ (kwadrat) jest 2-spójny krawędziowo (bo trzeba usunąć co najmniej 2 krawędzie, by go rozłączyć), ale nie jest 3-spójny krawędziowo (bo już 2 krawędzie wystarczą do rozspojenia).

**Spójność wierzchołkowa** grafu spójnego $G$ to najmniejsza liczba wierzchołków, jaką należy usunąć (z krawędziami incydentnymi), aby graf przestał być spójny. Oznaczamy ją $\kappa(G)$. Innymi słowy, $\kappa(G)$ to rozmiar najmniejszego *zbioru rozdzielającego* wierzchołków. Jeżeli $\kappa(G) \ge k$, to graf jest nazywany **$k$-spójnym (wierzchołkowo)**. Np. $C\_4$ jest 2-spójny (bo usunięcie jednego wierzchołka wciąż pozostawia graf spójnym – powstaje ścieżka $P\_3$), ale nie jest 3-spójny (usunięcie dwóch wierzchołków już zawsze rozspoi).

## Grafy Eulerowskie
**Cykl Eulera** to cykl, który przechodzi przez *każdą krawędź grafu dokładnie raz*. **Graf eulerowski** to graf, który *posiada* cykl Eulera. Mówi się obrazowo, że taki graf da się “narysować jedną kreską”, wracając do punktu startowego, nie podnosząc ołówka z papieru i nie rysując żadnej krawędzi więcej niż raz (nawiązanie do klasycznego problemu mostów Königsberga).

**Ścieżka Eulera** (droga Eulera) to ścieżka przechodząca przez każdą krawędź grafu dokładnie raz (ale *niekoniecznie wracająca do punktu startu*). Graf posiadający ścieżkę Eulera nazywamy **pół-eulerowskim** (ślad Eulera istnieje, lecz nie jest cyklem).

**Twierdzenie Eulera:** *Spójny* graf nieskierowany jest eulerowski wtedy i tylko wtedy, gdy każdy jego wierzchołek ma parzysty stopień. Innymi słowy, warunkiem koniecznym i wystarczającym istnienia cyklu Eulera jest brak wierzchołków o nieparzystym stopniu (w spójnym grafie).

* **Wniosek 1:** Spójny graf eulerowski można rozłożyć na rozłączne cykle obejmujące wszystkie jego krawędzie (intuicyjnie: cykl Eulera sam jest takim rozłożeniem, ale twierdzenie gwarantuje też rozkład na cykle w grafach z kilkoma cyklami składowymi).

* **Wniosek 2:** Spójny graf jest pół-eulerowski (posiada ścieżkę Eulera, lecz niekoniecznie cykl) wtedy i tylko wtedy, gdy dokładnie dwa wierzchołki mają stopień nieparzysty. W takim przypadku każda ścieżka Eulera zaczyna się w jednym z tych dwóch wierzchołków nieparzystych, a kończy w drugim.

> **Przykład:** Graf złożony z dwóch trójkątów połączonych jednym mostem (dwóch $C\_3$ złączonych w szereg) nie jest eulerowski – most ma dwa końce o stopniu nieparzystym (3 i 3), co łamie warunek. Jest jednak pół-eulerowski (ma ścieżkę Eulera zaczynającą się i kończącą w wierzchołkach o nieparzystym stopniu). Gdybyśmy dodali jeszcze jedną krawędź łączącą te dwa wierzchołki nieparzyste, oba stałyby się stopnia parzystego i graf stałby się eulerowski (cykl Eulera istnieje).

**Algorytm znajdowania cyklu Eulera:** istnieje prosty algorytm (Fleury’ego) do wyznaczenia cyklu Eulera – opiera się on na przechodzeniu grafu i wybieraniu **niefatalnych** krawędzi (to jest takich, których usunięcie nie rozspaja pozostałości grafu) aż do przejścia wszystkimi krawędziami.

W przypadku **grafów skierowanych** pojęcia są analogiczne: cykl Eulera to cykl obejmujący wszystkie łuki, graf eulerowski – posiadający cykl Eulera, itd. Warunki na istnienie cyklu Eulera w spójnym (silnie spójnym) digrafie są następujące: każdy wierzchołek musi mieć równy stopień wejściowy i wyjściowy (w każdym “wchodzi” tyle samo, ile “wychodzi”), a ponadto wszystkie wierzchołki o niezerowym stopniu muszą należeć do jednej silnie spójnej składowej. Analogicznie, istnienie ścieżki Eulera w digrafie wymaga, aby *dokładnie dwa* wierzchołki miały różnicę stopni wejściowego i wyjściowego równą $\pm 1$ (jeden ma o jeden większy outdeg, drugi o jeden większy indeg), a pozostałe miały równe stopnie, przy spełnieniu warunku silnej spójności po dodaniu brakującego łuku między tymi dwoma wierzchołkami.

## Grafy Hamiltonowskie

**Cykl Hamiltona** to cykl w grafie prostym, który **przechodzi przez każdy wierzchołek dokładnie raz** (poza oczywiście powtarzającym się początkowo-końcowym wierzchołkiem). **Graf Hamiltona** to graf zawierający cykl Hamiltona. Analogicznie **ścieżka Hamiltona** to ścieżka przechodząca przez wszystkie wierzchołki grafu dokładnie raz (nie będąca cyklem), a graf posiadający ścieżkę Hamiltona nazywamy **pół-hamiltonowskim**.

W przeciwieństwie do grafów eulerowskich, nie istnieje proste kryterium rozpoznawania grafów hamiltonowskich. Problem **stwierdzenia, czy graf jest Hamiltonowski**, jest znany jako NP-zupełny – nie znamy wielomianowego algorytmu, który w ogólności znajduje cykl Hamiltona lub orzeka jego brak. O ile warunek eulerowski (parzystość stopni) daje się łatwo sprawdzić, o tyle dla Hamiltonowskości znane są tylko pewne *warunki wystarczające*.

Przykładowo, **twierdzenie Diraca** głosi: jeśli graf prosty ma $n \ge 3$ wierzchołki i każdy wierzchołek ma stopień **co najmniej** $n/2$, to graf jest Hamiltonowski. Z kolei **twierdzenie Ore’ego**: jeśli graf prosty na $n \ge 3$ wierzchołkach spełnia, że dla dowolnych dwóch **niepołączonych** wierzchołków $v$ i $w$ zachodzi $deg(v) + deg(w) \ge n$, to graf jest Hamiltonowski. Są to jednak tylko warunki wystarczające – ich niespełnienie nie przesądza o braku cyklu Hamiltona, a spełnienie gwarantuje istnienie cyklu Hamiltona. W praktyce rozpoznawanie Hamiltonowskości często opiera się na przeszukiwaniu z nawrotami (backtracking) lub heurystykach.

> **Przykład:** Graf pełny $K\_n$ jest oczywiście Hamiltonowski (wprost mamy $(n-1)!/2$ cykli Hamiltona). Graf dwudzielny $K\_{m,n}$ jest Hamiltonowski wtedy, gdy $|m-n| = 0$ (dla cyklu) lub $1$ (dla ścieżki pół-hamiltonowskiej) – np. $K\_{3,3}$ ma cykl Hamiltona, a $K\_{4,3}$ ma jedynie ścieżkę Hamiltona, natomiast $K\_{5,3}$ nie ma nawet ścieżki Hamiltona, bo jedna ze stron jest zbyt “liczna”. Graf Petersena, mimo że dość gęsty, **nie posiada** cyklu Hamiltona.

*(Grafy Hamiltonowskie pojawiają się m.in. w kontekście problemu komiwojażera. W ramach podstaw egzaminacyjnych należy znać definicje i umieć wskazać lub skonstruować cykl/ścieżkę Hamiltona w prostych przypadkach, ale złożone własności i twierdzenia jak Diraca czy Ore’ego są poza minimalnym zakresem.)*

## Drzewa (grafy acykliczne spójne)

**Drzewo** to graf **spójny**, który **nie zawiera cykli** (acykliczny). Graf acykliczny, który nie jest koniecznie spójny, nazywamy **lasem** (każda składowa lasu jest drzewem). Innymi słowy: drzewo jest grafem, w którym istnieje dokładnie jedna ścieżka między każdą parą różnych wierzchołków. Wierzchołek drzewa o stopniu 1 (czyli mający tylko jednego sąsiada) nazywamy **liściem**; pozostałe (stopnia $\ge 2$) nazywa się **wierzchołkami wewnętrznymi**. (W teorii drzew często używa się też terminu “węzeł” jako synonimu wierzchołka, zwłaszcza gdy myślimy o drzewach ukorzenionych.)

**Charakterystyka drzew:** Dla każdego grafu $T$ z $n$ wierzchołkami następujące warunki są równoważne (tj. każde z tych stwierdzeń definiuje drzewo):

1. $T$ jest spójny i acykliczny (definicja drzewa).
2. $T$ jest spójny i ma dokładnie $n-1$ krawędzi.
3. $T$ nie zawiera cykli i ma dokładnie $n-1$ krawędzi.
4. Każda krawędź $T$ jest mostem (usunięcie dowolnej krawędzi rozspaja graf).
5. Dla każdych dwóch różnych wierzchołków $u, v \in V(T)$ istnieje *dokładnie jedna* ścieżka $u$–$v$ w grafie $T$.
6. Dodanie do $T$ jednej dowolnej brakującej krawędzi (między dwoma wierzchołkami, które wcześniej nie były połączone bezpośrednio) tworzy dokładnie jeden cykl.

Z powyższych własności wynika kilka ważnych faktów o drzewach:

* Każde drzewo o co najmniej jednej krawędzi ma **co najmniej 2 liście**. (Dowód: jeśli drzewo $T$ jest spójne i ma $n-1$ krawędzi, to średni stopień wierzchołka wynosi $\frac{2(n-1)}{n} < 2$. W związku z tym w $T$ musi istnieć wierzchołek stopnia 1; usunięcie go i indukcyjna argumentacja dowodzi istnienia przynajmniej dwóch liści.)

* Jeśli graf jest lasem złożonym z $k$ składowych (czyli składa się z $k$ drzew), to ma on dokładnie $n - k$ krawędzi. W szczególności każde drzewo ($k=1$) na $n$ wierzchołkach ma $n-1$ krawędzi, co zgadza się z powyższą charakterystyką.

* Suma stopni wszystkich wierzchołków w drzewie o $n$ wierzchołkach wynosi $2(n-1)$. 

* W drzewie o co najmniej 2 wierzchołkach zawsze istnieją **co najmniej dwa liście** (wspomniane wyżej). Ponadto w drzewie o co najmniej 3 wierzchołkach możemy wyróżnić tzw. **centrum drzewa** – jest to pojedynczy wierzchołek (lub krawędź), który leży “najbliżej wszystkich innych”. Dokładniej, centrum to zbiór wierzchołków o minimalnej *ekscenctryczności* (najmniejszej maksymalnej odległości do innych); w drzewie centrum stanowi albo pojedynczy wierzchołek, albo dwuwierzchołkową krawędź (gdy drzewo ma parzystą średnicę). Wynika stąd np. że drzewo o $\ge 3$ wierzchołkach ma co najmniej 2 liście i co najwyżej 2 liście “po przeciwległych stronach”. (To twierdzenie Jordana, niekoniecznie wymagane na najniższą ocenę.)

> **Indeks Wienera** (opcjonalnie): sumę odległości pomiędzy wszystkimi parami wierzchołków grafu $G$ nazywamy indeksem Wienera $W(G)$. Można wykazać, że spośród wszystkich drzew o danej liczbie wierzchołków $n$, minimalny indeks Wienera ma graf najbardziej “gwiaździsty” (gwiazda $K\_{1,n-1}$), a maksymalny – graf najbardziej wydłużony (ścieżka $P\_n$).

**Drzewa etykietowane i kod Prüfera:** Drzewo *etykietowane* na $n$ wierzchołkach to takie, w którym wierzchołki mają unikalne etykiety (np. liczby $1,...,n$).
 **Twierdzenie Cayleya:** istnieje $n^{,n-2}$ różnych etykietowanych drzew na $n$ wierzchołkach. To klasyczny wynik teorii grafów, którego dowód opiera się na tzw. *kodzie Prüfera*.
  **Kod Prüfera** to sposób jednoczesnego policzenia i zakodowania wszystkich drzewa etykietowanych: każdemu drzewu przyporządkowuje się w bijektywny sposób ciąg $(n-2)$ liczb z zakresu $1...n$, co pokazuje, że liczba drzew wynosi $n^{,n-2}$.

**Drzewa ukorzenione i binarne:** Często przydatne jest wyróżnienie w drzewie jednego wierzchołka jako **korzenia**. *Drzewo ukorzenione* to po prostu drzewo z takim wyróżnionym wierzchołkiem. Korzeń wprowadza pojęcia poziomów, rodziców i dzieci – w drzewie ukorzenionym możemy mówić, że jeden wierzchołek jest **potomkiem** (dzieckiem, wnukiem, itd.) innego. **Drzewo binarne** to z kolei drzewo (zwykle ukorzenione), w którym każdy węzeł może mieć najwyżej dwoje dzieci (lewe i prawe). Drzewa binarne odgrywają istotną rolę w informatyce (np. drzewa poszukiwań binarnych BST, kopce, drzewo Huffmana), ale szczegóły tych zastosowań nie są wymagane na najniższą ocenę.

* **Drzewa ukorzenione:** jeśli w drzewie wyróżnimy jeden wierzchołek jako **korzeń**, to uzyskamy *drzewo ukorzenione*. W drzewie takim wprowadza się pojęcie **hierarchii** i relacji rodzinnych: dla każdego wierzchołka $v$ możemy zdefiniować:

  * **głębokość** (poziom) $v$: odległość od korzenia (długość unikalnej ścieżki z korzenia do $v$),
  * **wysokość drzewa**: maksymalna głębokość występująca w drzewie (długość najdłuższej ścieżki od korzenia do liścia),
  * **przodek i potomek:** jeśli $w$ leży na drodze od korzenia do $v$ (łącznie z korzeniem i $v$ samym), to $w$ jest przodkiem $v$, a $v$ potomkiem $w$,
  * **rodzic** (ojciec) i **dziecko** (syn): jeśli $w$ jest najbliższym przodkiem $v$ (tuż nad $v$), to $w$ jest rodzicem, a $v$ jego dzieckiem,
  * **rodzeństwo:** dwa wierzchołki mające wspólnego rodzica nazywamy braćmi (bliźniakami),
  * **liście:** w drzewie ukorzenionym to nadal wierzchołki bez dzieci (stopień 1 w drzewie nieskierowanym),
  * **poddrzewo** zakorzenione wierzchołka $v$: drzewo utworzone przez $v$ oraz wszystkich jego potomków (i krawędzie między nimi).
* **Liczby Catalana:** w kontekście drzew pojawiają się też *liczby Catalana*, które zliczają m.in. różne struktury drzewiczne. Przykładowo, liczba różnych drzew **binarnego** (z dokładnie dwoma poddrzewami w każdym węźle wewnętrznym) o $n$ węzłach wynosi $\frac{1}{n+1}\binom{2n}{,n}$ – jest to $n$-ta liczba Catalana. Liczby te opisują np. liczbę możliwych kształtów drzew poszukiwań binarnych, krotek pełnego zbalansowania nawiasów, itp.

* **Drzewa binarne i $d$-arne:** *drzewo binarne* to drzewo ukorzenione, w którym każdy węzeł może mieć najwyżej dwoje dzieci (najczęściej rozróżnia się **lewe** i **prawe** dziecko). Ogólniej, *drzewo $d$-arne* to drzewo, gdzie każdy wierzchołek ma co najwyżej $d$ dzieci. *Pełne drzewo $d$-arne* wysokości $h$ ma maksymalną liczbę węzłów na wszystkich poziomach z wyjątkiem może ostatniego – w pełnym drzewie binarnym każdy węzeł ma 0 lub $d$ dzieci, a liście występują tylko na dwóch najniższych poziomach (ostatni może być nie w pełni zapełniony). Liczba węzłów pełnego drzewa $d$-arnego wysokości $h$ wynosi w przybliżeniu $\frac{d^{,h+1}-1}{d-1}$ (suma ciągu geometrycznego).

* **Drzewo uporządkowane:** drzewo $d$-arne, w którym dzieci każdego węzła są ułożone w określonym porządku (np. od lewej do prawej). W drzewie uporządkowanym możemy mówić np. o „pierwszym” i „ostatnim” dziecku danego węzła. Standardowy *porządek leksykograficzny* węzłów drzewa uporządkowanego to np. porządek poziomami od lewej do prawej.



## Planarność

* **Graf planarny:** graf jest *planarny*, jeśli można go narysować na płaszczyźnie tak, aby żadne krawędzie się nie przecinały (poza wierzchołkami, w których się spotykają). Taki rysunek nazywamy **rysunkiem płaskim** grafu. Grafy planarne to np. wszystkie drzewa, grafy planarnych wielościanów (sześcian jako graf $Q\_3$, itp.). Graf, którego nie da się narysować bez przecięć, nazywa się *nieplanarny*.

* **Twierdzenie Kuratowskiego:** graf $G$ jest planarny **wtedy i tylko wtedy**, gdy nie zawiera podgrafu *homeomorficznego* z grafem $K\_5$ (kompletnym grafem na 5 wierzchołkach) ani z grafem $K\_{3,3}$ (kompletnym dwudzielnym na 3+3 wierzchołkach). Homeomorficzne oznacza tu, że z $G$ można otrzymać $K\_5$ lub $K\_{3,3}$ przez *kurczenie* (ściśnięcie) pewnych krawędzi i ewentualne pomijanie zbędnych wierzchołków stopnia 2. W praktyce $K\_5$ i $K\_{3,3}$ to tzw. **grafy Kuratowskiego** – oba są nieplanarne i każda inna nieplanarność zawiera je w pewnej „ukrytej” formie. Przykładowo graf Petersena jest nieplanarny, bo zawiera podgraf homeomorficzny $K\_{3,3}$.

* **Twierdzenie Eulera dla grafów planarnych:** dla każdego spójnego grafu planarnego zachodzi zależność między liczbą wierzchołków $n$, krawędzi $m$ i ścian $f$ w dowolnym jego płaskim narysowaniu: **$n - m + f = 2$**. (Tutaj *ściany* to obszary płaszczyzny rozdzielone krawędziami grafu, w tym jedna *ściana nieskończona* obejmująca „zewnętrzny” obszar poza rysunkiem grafu.) Wniosek: w każdym rysunku spójnego grafu planarnego liczby $n,m,f$ spełniają powyższy związek i w szczególności $f$ jest jednoznacznie wyznaczone przez $n$ i $m$. 

Z twierdzenia Eulera wynikają dalsze ograniczenia: np. **dla prostego grafu planarnego** z $n\ge 3$ wierzchołkami maksymalna liczba krawędzi wynosi $m\_{\max}=3n-6$. Jeśli graf planarny nie ma trójkątów (cykli długości 3), to $m\_{\max}=2n-4$. Z tego np. wynika od razu, że $K\_5$ (ma $5$ wierzchołków i $10$ krawędzi) nie może być planarny, bo $10 > 3\cdot 5 - 6 = 9$, podobnie $K\_{3,3}$ (6 wierzchołków, 9 krawędzi, ale brak trójkątów – powinno być $m \le 2\cdot6-4=8$) – to alternatywne uzasadnienie nieplanarności tych grafów.

* **Liczba przecięć (crossing number):** dla grafu nieplanarnego można zdefiniować jego **liczbę przecięć** $cr(G)$ jako minimalną liczbę punktów, w których krawędzie muszą się przecinać na płaszczyźnie przy *najlepszym* możliwym rysunku grafu. Planarne grafy mają $cr(G)=0$. Np. $cr(K\_5)=1$ i $cr(K\_{3,3})=1$ (oba da się narysować z tylko jednym przecięciem). Im większa liczba przecięć, tym „bardziej nieplanarny” jest graf – można to traktować jako miarę złożoności planarnych rysunków grafu.

* **Grubość grafu:** *grubością* $t(G)$ grafu nazywamy najmniejszą liczbę warstw (rysunków płaskich), na jakie można rozłożyć krawędzie grafu $G$ tak, by na każdej warstwie osobno graf był planarny. Inaczej, jest to minimalna liczba planarów, których suma (nakładając krawędzie) daje dany graf. Przykład: $K\_5$, $K\_{3,3}$ i $K\_6$ mają grubość $t(G)=2$ – ich krawędzie można rozdzielić na dwa planarne podgrafy. Grubość ma zastosowania np. przy projektowaniu wielowarstwowych obwodów drukowanych (ile płyt potrzeba, by poprowadzić wszystkie połączenia bez przecinania się ścieżek).

* **Grafy dualne:** każdemu spójnemu grafowi planarnemu w danym rysunku można przyporządkować graf *dualny* $G^*$: umieszczamy jeden wierzchołek w każdej ścianie oryginalnego rysunku, a dla każdej krawędzi grafu oryginalnego rysujemy łuk łączący dwa wierzchołki dualne leżące w ścianach rozdzielanych przez tę krawędź (łuk przechodzi przez tę krawędź, np. „przecina ją”). Graf dualny $G^*$ ma więc tyle wierzchołków ile $G$ ma ścian i tyle krawędzi ile $G$ ma krawędzi. Dualność ma własność $G^{**} \cong G$ (dual do dualnego jest izomorficzny do wyjściowego grafu) o ile $G$ jest spójny. Uwaga: dualny graf konkretnego rysunku może zawierać wielokrotne krawędzie (np. jeśli dwie ściany są rozdzielone kilkoma krawędziami w $G$) – dlatego czasem rozróżnia się **dualność abstrakcyjną** niezależną od rysunku.

* **Cykle i rozcięcia – dualność:** *rozcięciem* (cut) w grafie nazywamy taki zbiór krawędzi, którego usunięcie zwiększa liczbę spójnych składowych (np. pojedyncza krawędź będąca *mostem* jest szczególnym przypadkiem rozcięcia). W grafach planarnych istnieje piękna symetria: **dowolny zbiór krawędzi tworzy cykl w grafie $G$ $\iff$ odpowiadający mu zbiór krawędzi w grafie dualnym $G^*$
 stanowi rozcięcie**. Innymi słowy, cykl w $G$ odpowiada pewnemu przecięciu dualnych krawędzi rozdzielających jakieś dwie części grafu dualnego, i odwrotnie każde rozcięcie w $G$ przekłada się na cykl w $G^*$. Ta *dualność cykli i rozcięć* jest bezpośrednim uogólnieniem obserwacji, że w płaskim grafie krawędź będąca mostem (rozcięcie jednoelementowe) w dualnym odpowiada pętli (cyklowi elementarnemu).

## Digrafy (grafy skierowane)

* **Orientowalność grafu nieskierowanego:** zastanówmy się, kiedy graf nieskierowany można *ukierunkowić* tak, aby stał się silnie spójny. Graf nieskierowany $G$ nazywamy **orientowalnym silnie**, jeśli można każdej jego krawędzi nadać pewien kierunek (zamienić na łuk), uzyskując digraf silnie spójny. **Twierdzenie:** spójny graf nieskierowany jest orientowalny (silnie) $\iff$ każda jego krawędź leży na jakimś cyklu (w grafie nieskierowanym). Równoważnie – graf orientowalny nie może mieć *mostów* (krawędzi rozcinających graf). Jest to intuicyjne: obecność mostu uniemożliwia silną łączność po skierowaniu – w jedną stronę przejazd będzie niemożliwy. 
*Szkic dowodu:* jeśli graf nie ma mostów, to wykonując na nim DFS możemy każdą krawędź drzewa DFS skierować z rodzica do dziecka, a każdą krawędź powrotną (która musiała istnieć, bo brak mostów) skierować z potomka do przodka – powstały digraf będzie silnie spójny.

* **Przykłady digrafów:** ważną klasą digrafów są **turnieje** – już wspomniane kompletne digrafy na $n$ wierzchołkach (każda para wierzchołków jest połączona jednym łukiem w jedną ze stron, jak mecz każdy z każdym). Turnieje są zawsze słabo spójne; co więcej, znane jest twierdzenie Rédei’ego: każdy turniej zawiera *ścieżkę Hamiltona*. Mocniejsze: **każdy silnie spójny turniej jest Hamiltonowski** (istnieje w nim cykl Hamiltona). W ogólności, problem Hamiltonowski dla ogólnych digrafów jest trudny, ale np. **twierdzenie Ghouila-Harary’ego**: jeśli spójny turniej (digraf pełny) ma pewną własność transitivity, to jest Hamiltonowski, etc.

## 7. Tematy dodatkowe
* *Stopnie wierzchołków:* w iloczynie kartezjańskim $\deg\_{G\_1 \times G\_2}(u,v) = \deg\_{G\_1}(u) + \deg\_{G\_2}(v)$. Wynika to z faktu, że z wierzchołka $(u,v)$ wychodzą krawędzie: wszystkie ze zmianą drugiej współrzędnej (tyle, ile ma $v$ sąsiadów w $G\_2$) oraz wszystkie ze zmianą pierwszej współrzędnej (tyle, ile $u$ ma sąsiadów w $G\_1$).
* *Odległości:* odległość między dwoma wierzchołkami $(u,v)$ i $(u',v')$ w $G\_1 \times G\_2$ okazuje się sumą odległości w składowych: $d\big((u,v), (u',v')\big) = d\_{G\_1}(u,u') + d\_{G\_2}(v,v')$. W szczególności **średnica** (maksymalna odległość między parami wierzchołków) spełnia $\mathrm{diam}(G\_1 \times G\_2) = \mathrm{diam}(G\_1) + \mathrm{diam}(G\_2)$ – najdalsze pary wierzchołków w iloczynie to kombinacje najdalszych par z każdego czynnika.


