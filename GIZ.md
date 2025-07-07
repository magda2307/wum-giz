
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

## Podgrafy i grafy indukowane

**Podgraf** grafu $G = (V, E)$ to graf $H = (V', E')$ taki, że $V' \subseteq V$ oraz $E' \subseteq E$. Innymi słowy, podgraf zawiera pewien podzbiór wierzchołków oryginalnego grafu oraz pewien podzbiór jego krawędzi.

**Podgraf indukowany** przez podzbiór wierzchołków $S \subseteq V$ to podgraf zawierający wszystkie wierzchołki z $S$ oraz *wszystkie* krawędzie oryginalnego grafu $G$, które łączą pary wierzchołków z $S$. Podgraf indukowany jest jednoznacznie wyznaczony przez zbiór $S$ – dodanie jakiejkolwiek krawędzi więcej spowodowałoby, że nie jest już indukowany przez samo $S$, a pominięcie jakiejkolwiek krawędzi łączącej wierzchołki z $S$ oznaczałoby, że nie jest maksymalny. Podgraf nieindukowany może zawierać tylko niektóre z krawędzi między wierzchołkami $S$.

> **Przykład:** Rozważmy graf $G$ będący kwadratem (cztery wierzchołki $a,b,c,d$ połączone w cykl). Podgrafem $G'$ na wierzchołkach ${a, b, c}$ może być np. ścieżka $a$–$b$–$c$ (dwie krawędzie spośród możliwych). Natomiast **podgraf indukowany** na wierzchołkach ${a, b, c}$ zawiera oprócz nich wszystkie krawędzie z $G$ mające końce w ${a, b, c}$. W oryginalnym grafie krawędziami takimi są $a$–$b$ oraz $b$–$c$, więc podgraf indukowany to dokładnie ścieżka $a$–$b$–$c$. (Innej krawędzi między tymi wierzchołkami w $G$ nie było, więc w tym wypadku akurat oba podgrafy się pokrywają.)

## Operacje na grafach

Na grafach definiuje się szereg operacji tworzących z nich nowe grafy:

* **Suma grafów $G\_1 \cup G\_2$:** graf, którego zbiorem wierzchołków jest suma zbiorów $V\_1 \cup V\_2$, a zbiorem krawędzi – suma $E\_1 \cup E\_2$. Intuicyjnie łączy dwa grafy, traktując je jako rozłączne (jeśli miały wspólne wierzchołki, w sumie traktuje się ich dwie kopie jako jeden wierzchołek).

* **Odjęcie krawędzi $G - e$:** usuwa z grafu $G$ krawędź $e$ (jeśli istnieje), pozostawiając resztę grafu bez zmian.

* **Odjęcie wierzchołka $G - v$:** usuwa wierzchołek $v$ wraz ze wszystkimi krawędziami incydentnymi z $v$. Wynikowy graf ma zbiór wierzchołków $V \setminus {v}$ i krawędzie $E$ bez tych incydentnych z $v$.

* **Ściągnięcie krawędzi $G \setminus e$ (kontrakcja):** usuwa krawędź $e={u,v}$ z grafu i **utożsamia** (scala) jej końce $u$ i $v$ w jeden wierzchołek. Wszystkie inne krawędzie dawniej incydentne z $u$ lub $v$ stają się incydentne z nowym połączonym wierzchołkiem. (Operacja ta zmniejsza liczbę wierzchołków o 1.)

* **Dodanie wierzchołka $G + v$:** do grafu $G$ dodajemy nowy wierzchołek $v$ (nieistniejący wcześniej w $V$) oraz opcjonalnie nowe krawędzie łączące go z wybranymi wierzchołkami oryginalnego grafu. Szczególnym przypadkiem jest dodanie **uniwersalnego** wierzchołka – dołączenie $v$ połączonego krawędziami ze *wszystkimi* dotychczasowymi wierzchołkami.

* **Dopełnienie grafu $G'$:** graf na tym samym zbiorze wierzchołków co $G$, w którym krawędź istnieje **tylko** tam, gdzie nie było jej w $G$. Formalnie, $G'$ ma zbiór wierzchołków $V$, a zbiór krawędzi to $E' = {{v,w}: v\neq w, {v,w}\notin E}$ (dla grafu prostego nieskierowanego).

* **Iloczyn kartezjański grafów $G\_1 \times G\_2$:** graf, w którym zbiór wierzchołków stanowi iloczyn kartezjański $V\_1 \times V\_2$, a dwa wierzchołki $(v\_i, w\_j)$ oraz $(v\_k, w\_l)$ są połączone krawędzią wtedy, gdy $i=k$ i ${w\_j, w\_l} \in E\_2$, *lub* $j=l$ i ${v\_i, v\_k} \in E\_1$. Intuicyjnie jest to graf, w którym budujemy “kratkę” łączącą dwa grafy: kopie pierwszego są powielone dla każdego wierzchołka drugiego grafu, a połączenia między kopiami odpowiadają krawędziom drugiego grafu, i vice versa.

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

*(Wymienione nazwy rodzin grafów warto kojarzyć z ich charakterystycznymi własnościami, jednak do podstawowego zakresu egzaminacyjnego należy głównie umiejętność rozpoznania i podania parametrów grafów takich jak $N\_n$, $K\_n$, $K\_{m,n}$, $P\_n$, $C\_n$, ewentualnie $W\_n$.)*

![alt text](image.png)
![alt text](image-1.png)
![alt text](image-2.png)
## Reprezentacje grafów

Graf można zapisać w pamięci komputera lub na papierze na różne sposoby – wybór **reprezentacji** wpływa na efektywność operacji i zużycie pamięci. Najważniejsze standardowe reprezentacje to:

* **Macierz sąsiedztwa:** dla grafu o $n$ wierzchołkach jest to kwadratowa macierz $A$ rozmiaru $n\times n$, gdzie na pozycji $(i,j)$ zapisujemy:

  * 1, jeśli między wierzchołkiem $i$ a $j$ istnieje krawędź;
  * 0, jeśli brak krawędzi między $i$ i $j$;
  * (dla grafów z pętlami: zwykle przyjmuje się wartość 2 na diagonali w miejscu pętli $(i,i)$).

  Macierz sąsiedztwa grafu nieskierowanego jest **symetryczna** względem diagonali ($A = A^T$). Dla grafu skierowanego macierz może być asymetryczna – jedynki w wierszu $i$ wskazują na krawędzie wychodzące z wierzchołka $i$, a jedynki w kolumnie $i$ – na krawędzie wchodzące do $i$. W macierzy sąsiedztwa **grafu prostego** wszystkie komórki na głównej przekątnej mają 0 (brak pętli).

  *Koszt pamięci:* Macierz sąsiedztwa zajmuje $Θ(n^2)$ pamięci niezależnie od liczby krawędzi. Jest to wydajne przy grafach **gęstych** (gdy $m$ jest rzędu $n^2$). 
  
  Niektóre operacje, np. sprawdzenie istnienia krawędzi między danymi wierzchołkami, są w tej reprezentacji bardzo szybkie (jedno indeksowanie tablicy).

* **Macierz incydencji:** tablica $n \times m$, w której wiersz odpowiada wierzchołkowi, a kolumna – krawędzi. W przypadku grafu nieskierowanego w komórce $(v, e)$ wpisujemy 1, jeśli krawędź $e$ jest incydentna z wierzchołkiem $v$, w przeciwnym razie 0. Dla grafu skierowanego przyjmuje się np. konwencję: 1 jeśli krawędź *wchodzi* do $v$, –1 jeśli *wychodzi* z $v$, 0 jeśli $v$ nie leży na tej krawędzi. Każda kolumna ma zatem dwie jedynki (lub jedynkę i minus jedynkę dla digrafu) – wskazujące końce danej krawędzi.

  *Koszt pamięci:* Macierz incydencji zajmuje $Θ(n \cdot m)$ komórek, co dla grafów rzadkich ($m = O(n)$) daje rząd $O(n^2)$ – zwykle mniej wydajny niż lista sąsiedztwa, a dla grafów gęstych ($m = Θ(n^2)$) rzędu $Θ(n^3)$, co czyni tę reprezentację bardzo kosztowną pamięciowo.

* **Lista sąsiedztwa:** dla każdego wierzchołka przechowujemy listę wszystkich wierzchołków, z którymi jest bezpośrednio połączony krawędzią. Implementacyjnie często jest to tablica list: indeks tablicy odpowiada etykiecie wierzchołka, a pod nim lista sąsiadów. Dla grafu skierowanego lista sąsiedztwa zwykle zawiera **następników** (wierzchołki, do których wychodzą krawędzie z bieżącego). Można też przechowywać osobno listy poprzedników (dla krawędzi wchodzących).

  *Koszt pamięci:* Lista sąsiedztwa zajmuje $Θ(n + m)$ pamięci – mały narzut na wierzchołki plus po jednym elemencie na każdą krawędź (lub dwa dla nieskierowanych, bo każda krawędź pojawia się na liście dwóch końców). Dla grafów **rzadkich** ($m = O(n)$) jest znacznie oszczędniejsza niż macierz sąsiedztwa (koszt liniowy zamiast kwadratowego).

* **Lista krawędzi:** lista (lub zbiór) wszystkich krawędzi grafu, zwykle zapisanych jako pary (dla grafu nieskierowanego) lub uporządkowane pary (dla skierowanego) wierzchołków. Często przedstawiana jako tabela dwóch kolumn: każda pozycja to $(u, v)$ oznaczające krawędź między $u$ a $v$. Ta reprezentacja jest prosta i czytelna dla człowieka oraz wygodna do zapisu tekstowego (np. każda krawędź w oddzielnej linii). Sprawdza się też dla grafów dynamicznie rosnących – łatwo dopisać nowy wiersz reprezentujący dodaną krawędź.

  *Koszt pamięci:* $Θ(m)$ par wierzchołków. Trudniej jednak uzyskać z takiej listy np. listę sąsiadów danego wierzchołka bez pełnego przeglądu listy.

> **Porównanie reprezentacji:** Macierz sąsiedztwa jest korzystna dla grafów gęstych – ma stały czas dostępu do informacji o każdej potencjalnej krawędzi, ale zawsze zajmuje $n^2$ komórek pamięci, nawet jeśli krawędzi jest mało. Lista sąsiedztwa adaptuje się do wielkości grafu – zajmuje pamięć rzędu $n+m$ (dla małej liczby krawędzi jest bardzo oszczędna), jednak pewne operacje (np. sprawdzenie istnienia konkretnej krawędzi) mogą wymagać przeszukania listy i trwać dłużej niż w macierzy. Macierz incydencji jest rzadziej używana – bywa przydatna w kontekstach algebraicznych (np. teoria grafów algebraiczna), ale pamięciowo jest najmniej efektywna. Listy krawędzi są prostym sposobem zapisu (np. w plikach) i ułatwiają iterowanie po wszystkich krawędziach, lecz nie pozwalają szybko odczytać sąsiadów danego wierzchołka bez dodatkowych struktur pomocniczych.

## Ścieżki i cykle w grafach

**Ścieżka (droga)** w grafie to sekwencja wierzchołków $(v\_0, v\_1, ..., v\_k)$ taka, że każdy kolejny wierzchołek jest połączony krawędzią z poprzednim. Formalnie, istnieje ciąg krawędzi $(e\_1, e\_2, ..., e\_k)$, gdzie $e\_i = {v\_{i-1}, v\_i}$ dla $i=1,...,k$. Ścieżkę można także określić jako **naprzemienny ciąg wierzchołków i krawędzi** rozpoczynający i kończący się wierzchołkiem: $v\_0, e\_1, v\_1, e\_2, ..., e\_k, v\_k$, gdzie każde $e\_i$ łączy $v\_{i-1}$ z $v\_i$. Długością ścieżki nazywamy liczbę występujących w niej krawędzi (przyjmujemy, że ścieżka długości 0 to pojedynczy wierzchołek bez krawędzi).

Ścieżka **prosta** (prosty łańcuch) to taka, w której *żadna krawędź nie powtarza się*. Często przyjmuje się dodatkowo, że w ścieżce prostej nie powtarzają się również wierzchołki (poza ewentualnie początkowym i końcowym w cyklu) – taka ścieżka jest wówczas nazywana **elementarną**. (Różne źródła różnie definiują te pojęcia, dlatego należy zwracać uwagę na kontekst definicji.)

**Cykl** to zamknięta ścieżka – ścieżka, w której $v\_0 = v\_k$ (czyli początek i koniec to ten sam wierzchołek), oraz która ma co najmniej 3 krawędzie. Analogicznie jak wyżej, **cykl prosty** nie powtarza krawędzi, a **cykl elementarny** – nie powtarza żadnego wierzchołka poza początkowo-końcowym. **Obwód** grafu to długość najkrótszego cyklu w grafie (jeśli graf nie zawiera żadnego cyklu, mówimy że obwód jest nieskończony).

> **Uwaga:** W wielu zadaniach dopuszcza się określenie “ścieżka” jako synonim ścieżki prostej. W niniejszych notatkach przez ścieżkę zwykle będziemy rozumieć ścieżkę prostą, chyba że zaznaczono inaczej.

## Spójność grafu

Graf niepusty nazywamy **spójnym**, jeśli każde dwa jego różne wierzchołki można połączyć pewną ścieżką. Równoważnie: graf jest spójny, jeśli nie da się jego wierzchołków podzielić na dwa niepuste zbiory tak, by *brakowało* krawędzi między tymi dwoma częściami (tzn. graf nie jest sumą dwóch niepołączonych grafów). 
**Składowa spójna** to maksymalny (największy) podgraf spójny grafu – innymi słowy, spójna “część” grafu zawierająca pewien podzbiór wierzchołków. Każdy graf można jednoznacznie rozłożyć na swoje składowe spójne; liczbę składowych spójnych oznaczamy $c(G)$. Graf spójny ma $c(G)=1$. Graf całkowicie niespójny (pusty) na $n$ wierzchołkach ma $c(G)=n$.

W przypadku **grafów skierowanych** rozróżniamy spójność *słabą* i *silną*. Graf **silnie spójny** (silnie spójny skierowany) to taki digraf, w którym dla każdej uporządkowanej pary **różnych** wierzchołków $u, v$ istnieje ścieżka *skierowana* od $u$ do $v$. Innymi słowy, z każdego wierzchołka da się dosć do każdego innego, *uwzględniając kierunki łuków*. Graf **słabo spójny** to graf skierowany, który jest spójny jeśli **pominąć kierunki** krawędzi, czyli zastąpić wszystkie łuki krawędziami nieskierowanymi – wtedy powstały graf nieskierowany jest spójny. Silna spójność pociąga za sobą słabą (graf silnie spójny jest oczywiście spójny po “zapomnieniu” kierunków), ale nie odwrotnie. **Składowe silnie spójne** i **składowe słabo spójne** definiuje się analogicznie jak w przypadku grafów nieskierowanych (maksymalne podgrafy silnie, względnie słabo spójne).

Przykładem grafu, który jest słabo spójny, lecz nie jest   silnie spójny, jest skierowane drzewo (tzw. arborescencja) – np. wszystkie krawędzie skierowane “w dół” od korzenia. Taki graf jako nieskierowany jest spójny (to zwykłe drzewo), ale nie ma drogi skierowanej od liścia do innego liścia.

**Most** (lub **krawędź artykulacji**, **krawędź rozspajająca**) to krawędź, której usunięcie zwiększa liczbę składowych spójnych grafu. Innymi słowy, jest to krawędź, której usunięcie rozłącza graf – stanowi ona jedyne połączenie między dwoma fragmentami grafu.

**Punkt artykulacji** (czyli **wierzchołek rozdzielający**) to wierzchołek, którego usunięcie (wraz z wszystkimi incydentnymi z nim krawędziami) zwiększa liczbę składowych grafu. Inaczej: wierzchołek, po którego usunięciu graf się rozpada – ten wierzchołek “spinał” dwie lub więcej części sieci. Pojęcie to dotyczy tylko grafów nieskierowanych (w digrafach analogiem jest *punkt artykulacji silnej spójności*, rzadziej rozważany).

**Spójność krawędziowa** grafu spójnego $G$ to najmniejsza liczba krawędzi, jaką należy usunąć, aby graf stał się niespójny (lub równoważnie: aby liczba składowych wzrosła). Tę liczbę oznacza się $\lambda(G)$. Formalnie, $\lambda(G)$ to liczność najmniejszego *zbioru rozspajającego* (zbioru krawędzi, którego usunięcie rozspaja graf). Jeśli $\lambda(G) \ge k$, mówimy że graf jest **$k$-spójny krawędziowo**. Przykładowo, graf cykliczny $C\_4$ (kwadrat) jest 2-spójny krawędziowo (bo trzeba usunąć co najmniej 2 krawędzie, by go rozłączyć), ale nie jest 3-spójny krawędziowo (bo już 2 krawędzie wystarczą do rozspojenia).

**Spójność wierzchołkowa** grafu spójnego $G$ to najmniejsza liczba wierzchołków, jaką należy usunąć (z krawędziami incydentnymi), aby graf przestał być spójny. Oznaczamy ją $\kappa(G)$. Innymi słowy, $\kappa(G)$ to rozmiar najmniejszego *zbioru rozdzielającego* wierzchołków. Jeżeli $\kappa(G) \ge k$, to graf jest nazywany **$k$-spójnym (wierzchołkowo)**. Np. $C\_4$ jest 2-spójny (bo usunięcie jednego wierzchołka wciąż pozostawia graf spójnym – powstaje ścieżka $P\_3$), ale nie jest 3-spójny (usunięcie dwóch wierzchołków już zawsze rozspoi).

> **Przykład zastosowania:** Pojęcia $\lambda(G)$ i $\kappa(G)$ mają znaczenie w projektowaniu sieci odpornych na awarie – określają ile połączeń lub węzłów musiałoby naraz ulec uszkodzeniu, by sieć przestała przekazywać informacje między pewnymi punktami. Sieci o wysokiej spójności są bardziej wytrzymałe na awarie.

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
*(Kod Prüfera oraz wynik Cayleya wykraczają poza podstawowy zakres – nie są wymagane na najniższą ocenę, ale stanowią ciekawe uzupełnienie teorii drzew.)*

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

* **Porządki przeszukiwania drzewa:** dla drzew ukorzenionych definiuje się trzy podstawowe sposoby odwiedzania węzłów:
  * *Pre-order (porządek przedorderowy)* – najpierw odwiedzamy (przetwarzamy) węzeł bieżący, następnie rekurencyjnie jego lewe poddrzewo i prawe poddrzewo.
  * *In-order (porządek w środku)* – najpierw rekurencyjnie przetwarzamy lewe poddrzewo, potem bieżący węzeł, następnie prawe poddrzewo.
  * *Post-order (porządek poorderowy)* – najpierw rekurencyjnie lewe i prawe poddrzewo, a na końcu węzeł bieżący.

  Dla przykładu, pre-order wydrukuje zawartość drzewa zaczynając od korzenia i przechodząc w głąb, zawsze najpierw węzeł, potem jego dzieci. In-order dla drzewa binarnego da posortowaną kolejność kluczy, jeśli drzewo spełnia własność BST (poszukiwań binarnych). Post-order często używany jest przy usuwaniu drzewa (najpierw usuń dzieci, potem węzeł). Przykład – dla drzewa binarnego z korzeniem A, lewym dzieckiem B i prawym C: pre-order: A, B, C; in-order: B, A, C; post-order: B, C, A.

## Przeszukiwanie grafu (BFS i DFS)

Wiele algorytmów na grafach polega na systematycznym odwiedzaniu wszystkich wierzchołków i krawędzi w pewnym zorganizowanym porządku. Dwa podstawowe schematy **przeszukiwania grafu** to **przeszukiwanie wszerz** (BFS – *Breadth-First Search*) i **przeszukiwanie w głąb** (DFS – *Depth-First Search*). Oba algorytmy przyjmują graf (np. w postaci list sąsiedztwa) oraz ewentualnie wyróżniony wierzchołek startowy.

### Algorytm BFS (przeszukiwanie wszerz)

BFS korzysta z kolejki (FIFO) i odkrywa graf poziomami, **równomiernie we wszystkich kierunkach** od wierzchołka startowego, według rosnącej odległości. Intuicyjnie, BFS najpierw odwiedza wszystkich sąsiadów startowego, potem sąsiadów tych sąsiadów, itd., tworząc warstwami tzw. *drzewo BFS*.

**Schemat:**

1. Oznacz wszystkie wierzchołki jako **nieodwiedzone** (białe). Ustaw odległości $d$ od startowego $s$ na nieskończoność (lub dużą liczbę), poza $d(s)=0$. Przygotuj pustą kolejkę.
2. Oznacz startowy wierzchołek $s$ jako odwiedzony (szary) i umieść go w kolejce.
3. Dopóki kolejka nie jest pusta:

   * zdejmij z kolejki wierzchołek $u$,
   * *przetwórz* $u$ (np. wypisz lub odnotuj, że został odwiedzony),
   * dla każdego sąsiada $v$ wierzchołka $u$: jeśli $v$ jest jeszcze nieodwiedzony (biały), to oznacz go jako odwiedzony (szary), zapisz jego odległość $d(v) = d(u)+1$ i poprzednika $p(v)=u$ i dodaj $v$ do kolejki.
   * po przetworzeniu wszystkich sąsiadów $u$, oznacz $u$ jako całkowicie przetworzony (czarny).
4. Koniec – gdy kolejka się opróżni, wszystkie wierzchołki osiągalne ze startowego zostały odwiedzone. Jeśli istnieją wierzchołki nieodwiedzone (graf niespójny), można wznowić BFS z któregoś z nich jako nowego startu, aby odwiedzić kolejną składową.

**Złożoność:** Każda krawędź i wierzchołek jest odwiedzana stałą liczbę razy, więc czas działania BFS to $O(|V| + |E|)$ – liniowy względem rozmiaru grafu.

**Własności:** BFS oblicza **najkrótsze odległości** od startowego wierzchołka $s$ do wszystkich innych (w grafie *nieważonym*) – po zakończeniu algorytmu dla każdego odwiedzonego wierzchołka $v$ odległość $d(v)$ jest równa długości najkrótszej ścieżki z $s$ do $v$. Ponadto z relacji poprzedników $p(v)$ tworzy się **drzewo rozpinające** (a właściwie las dla niespójnego grafu) – tzw. *drzewo BFS*, które zawiera krawędzie ${p(v), v}$ dla każdego odwiedzonego $v \neq s$. Krawędzie grafu możemy podzielić na **drzewowe** (wchodzące w skład drzewa BFS) oraz **poprzeczne**, które łączą pewne dwa wierzchołki z różnych gałęzi/warstw drzewa BFS (w BFS nie występują krawędzie typu “do przodu” ani “wsteczne” w sensie klasyfikacji DFS).

> **Zastosowania BFS:** Oprócz obliczania odległości w grafie nieważonym (problem najkrótszej ścieżki), BFS pozwala także m.in.:
>
> * wyznaczać spójne składowe grafu (każde drzewo BFS to jedna składowa),
> * znaleźć cykl o minimalnej długości (jeśli podczas BFS natrafimy na krawędź poprzeczną, łączy ona dwa wierzchołki oddalone od $s$ o odległości $d$ i $d$ lub $d$ i $d+1$, co daje cykl długości $2d+1$ lub $2d+2$),
> * znaleźć graf powiązań o odległości $\le 2$ (domknięcie przekątne relacji) – wystarczy przeprowadzić BFS z każdym wierzchołkiem jako startowym (alternatywnie mnożenie macierzy sąsiedztwa),
> * stwierdzić dwudzielność grafu – jeśli podczas BFS uda się pokolorować graf dwoma kolorami warstwami (naprzemiennie), to graf jest dwudzielny. Jeśli pojawi się krawędź łącząca dwa wierzchołki z tej samej warstwy, to graf nie jest dwudzielny (występuje cykl nieparzysty).

### Algorytm DFS (przeszukiwanie w głąb)

DFS korzysta ze stosu (jawnie lub poprzez rekurencję) i eksploruje graf **jak najgłębiej**, cofając się dopiero, gdy dotrze do końca ścieżki. W efekcie DFS zagłębia się od wierzchołka startowego tak długo, aż napotka wierzchołek bez nieodwiedzonych sąsiadów, wtedy się cofa i szuka pierwszego napotkanego jeszcze nieodwiedzonego sąsiada, itd.

**Schemat (rekurencyjny):**

1. Oznacz wszystkie wierzchołki jako nieodwiedzone (białe) i wyzeruj licznik czasu.
2. Dla każdego wierzchołka $u$:

   * Jeśli $u$ jest nieodwiedzony, wykonaj wywołanie `DFSVisit(u)`:

     1. Zaznacz $u$ jako odwiedzony (szary), zapisz czas odkrycia $u.d =$ kolejny czas++.
     2. *Przetwórz* $u$ (np. odnotuj w porządku pre-order).
     3. Dla każdego sąsiada $v$ wierzchołka $u$:

        * Jeśli $v$ jest biały (nieodkryty) – zapisz $p(v)=u$ i wykonaj rekurencyjnie `DFSVisit(v)` (zagłębienie się krawędzią drzewową).
        * (Jeśli $v$ jest szary lub czarny – krawędź $(u,v)$ nie jest drzewowa; klasyfikacja poniżej.)
     4. Oznacz $u$ jako przetworzony (czarny); zapisz czas zakończenia $u.f =$ kolejny czas++.
3. Koniec – wszystkie osiągalne wierzchołki zostały odwiedzone; ewentualnie DFS podejmie się ponownie z innego wierzchołka, aby przetworzyć kolejną składową niespójnego grafu.

**Złożoność:** Podobnie jak BFS, DFS odwiedza każdą krawędź i wierzchołek stałą liczbę razy; złożoność wynosi $O(|V| + |E|)$.

W grafach **nieskierowanych** DFS generuje tylko krawędzie drzewowe i wsteczne. W grafach **skierowanych** mogą wystąpić wszystkie cztery rodzaje krawędzi.

Dla dowolnych dwóch wierzchołków $u, v$ zachodzi ciekawa własność tzw. **struktury nawiasowej**: ich przedziały czasowe przetwarzania albo są rozłączne, albo jeden zawiera się w drugim. To oznacza, że jeśli $u$ zostanie odkryty przed $v$ ($u.d < v.d$), to albo zakończy się przetwarzanie $u$ przed odkryciem $v$ ($u.f < v.d$), albo $u$ zakończy się po $v$ ($u.d < v.d < v.f < u.f$). Na tej podstawie można wykrywać cykle, tworzyć porządek topologiczny i znajdować silnie spójne komponenty.

**Zastosowania DFS:**

* **Sortowanie topologiczne** – wykonywane jest przez DFS w grafach acyklicznych skierowanych (DAG). Wystarczy wykonać DFS i zapisać wierzchołki w kolejności malejących czasów ukończenia $v.f$ – otrzymany porządek jest topologicznym uszeregowaniem DAG.
* **Silnie spójne składowe** – można wykryć dwukrotnie wykonując DFS (algorytm Kosaraju) albo jednym przebiegiem zmodyfikowanego DFS (algorytm Tarjana). Oba algorytmy wykraczają jednak poza podstawowy zakres.
* **Mosty i punkty artykulacji** – za pomocą DFS można w czasie liniowym wykryć wszystkie mosty i punkty artykulacji grafu. Wymaga to analizy drzew DFS i krawędzi wstecznych (algorytm oparty na tzw. wartościach low-link). Jest to zagadnienie bardziej złożone, omawiane zwykle na wyższych ocenach.
* **Rozwiązywanie zagadnień typu labirynt** – DFS nadaje się do przeszukiwania grafu w celu znalezienia ścieżki z punktu A do B (niekoniecznie najkrótszej, ale istniejącej). W praktyce jednak BFS częściej zapewnia ścieżki optymalne (najkrótsze).


## Planarność

* **Graf planarny:** graf jest *planarny*, jeśli można go narysować na płaszczyźnie tak, aby żadne krawędzie się nie przecinały (poza wierzchołkami, w których się spotykają). Taki rysunek nazywamy **rysunkiem płaskim** grafu. Grafy planarne to np. wszystkie drzewa, grafy planarnych wielościanów (sześcian jako graf $Q\_3$, itp.). Graf, którego nie da się narysować bez przecięć, nazywa się *nieplanarny*.

* **Twierdzenie Kuratowskiego (charakteryzacja planarności):** graf $G$ jest planarny **wtedy i tylko wtedy**, gdy nie zawiera podgrafu *homeomorficznego* z grafem $K\_5$ (kompletnym grafem na 5 wierzchołkach) ani z grafem $K\_{3,3}$ (kompletnym dwudzielnym na 3+3 wierzchołkach). Homeomorficzne oznacza tu, że z $G$ można otrzymać $K\_5$ lub $K\_{3,3}$ przez *kurczenie* (ściśnięcie) pewnych krawędzi i ewentualne pomijanie zbędnych wierzchołków stopnia 2. W praktyce $K\_5$ i $K\_{3,3}$ to tzw. **grafy Kuratowskiego** – oba są nieplanarne i każda inna nieplanarność zawiera je w pewnej „ukrytej” formie. Przykładowo graf Petersena jest nieplanarny, bo zawiera podgraf homeomorficzny $K\_{3,3}$.

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

**Iloczyn kartezjański grafów:** dla dwóch grafów $G\_1=(V\_1,E\_1)$ oraz $G\_2=(V\_2,E\_2)$, ich iloczyn kartezjański $G = G\_1 \times G\_2$ zdefiniowano w sekcji 1. Tutaj dodajmy jego podstawowe własności:

* *Stopnie wierzchołków:* w iloczynie kartezjańskim $\deg\_{G\_1 \times G\_2}(u,v) = \deg\_{G\_1}(u) + \deg\_{G\_2}(v)$. Wynika to z faktu, że z wierzchołka $(u,v)$ wychodzą krawędzie: wszystkie ze zmianą drugiej współrzędnej (tyle, ile ma $v$ sąsiadów w $G\_2$) oraz wszystkie ze zmianą pierwszej współrzędnej (tyle, ile $u$ ma sąsiadów w $G\_1$).
* *Odległości:* odległość między dwoma wierzchołkami $(u,v)$ i $(u',v')$ w $G\_1 \times G\_2$ okazuje się sumą odległości w składowych: $d\big((u,v), (u',v')\big) = d\_{G\_1}(u,u') + d\_{G\_2}(v,v')$. W szczególności **średnica** (maksymalna odległość między parami wierzchołków) spełnia $\mathrm{diam}(G\_1 \times G\_2) = \mathrm{diam}(G\_1) + \mathrm{diam}(G\_2)$ – najdalsze pary wierzchołków w iloczynie to kombinacje najdalszych par z każdego czynnika.

**Metryka sieciowa w grafach:** W grafach definiujemy kilka pojęć mierzących „odległości” w sieci (przy założeniu spójności w danej analizowanej składowej):
* *Odległość $d(u,v)$:* długość najkrótszej ścieżki między wierzchołkami $u$ i $v$. Jeśli wierzchołki są w różnych składowych, można przyjąć $d(u,v)=\infty$.
* *Ekscentryczność $e(v)$:* maksymalna odległość od wierzchołka $v$ do dowolnego innego wierzchołka grafu (tj. $e(v) = \max\_{u\in V}d(v,u)$). Mówi jak „daleko” w najgorszym razie jest $v$ od reszty.
* *Promień grafu $r(G)$:* najmniejsza ekscentryczność w grafie, $r(G) = \min\_{v\in V} e(v)$. Jest to odległość od najbardziej centralnego wierzchołka do reszty – czyli minimalny zasięg, w jakim można „objąć” wszystkie wierzchołki z jednego miejsca.
* *Średnica grafu $\mathrm{diam}(G)$:* największa ekscentryczność, $\mathrm{diam}(G) = \max\_{v\in V} e(v)$, czyli najdłuższa odległość jaka występuje między jakąkolwiek parą wierzchołków.
* *Centrum grafu:* zbiór wierzchołków o ekscentryczności równej promieniowi (${v: e(v)=r(G)}$). Wierzchołki centralne to te, które są minimalnie oddalone od wszystkich pozostałych. Dla drzew centrum to pojedynczy wierzchołek lub dwa wierzchołki (gdy drzewo ma parzystą średnicę – leżące w środku najdłuższej ścieżki; por. twierdzenie Jordana wcześniej).

**Algorytmy grafowe – przeszukiwanie grafu:** wiele algorytmów operuje na grafach poprzez **przeszukiwanie** – systematyczne odwiedzanie wierzchołków i krawędzi. Istnieją dwie podstawowe strategie:

* **BFS (Breadth-First Search, przeszukiwanie wszerz):** rozpoczyna od zadanego wierzchołka startowego i odwiedza najpierw wszystkich jego sąsiadów, potem sąsiadów sąsiadów itd., warstwami. Implementacja BFS używa kolejki: najpierw do kolejki trafia start, następnie w pętli zdejmujemy z kolejki wierzchołek, odwiedzamy go i wszystkich nieodwiedzonych sąsiadów dodajemy do kolejki. BFS wyznacza tzw. *drzewo przeszukiwania* (spanning tree) warstwowe. **Złożoność BFS to $O(|V|+|E|)$** – liniowa względem rozmiaru grafu. Zastosowania BFS: wyznaczanie najkrótszych ścieżek w grafach **nieważonych** (od startu do wszystkich wierzchołków), sprawdzanie spójności (osiągalności wierzchołków), znajdowanie cykli parzystych (graf jest bipartytowy $\iff$ BFS nie wykryje konfliktu dwukolorowania warstw) itp.

* **DFS (Depth-First Search, przeszukiwanie w głąb):** strategia odwrotna do BFS – zagłębia się jak najdalej w graf od startu, cofa kiedy napotka już odwiedzony wierzchołek lub brak sąsiadów do eksploracji. Implementacja zwykle rekurencyjna lub ze stosem: zaczynamy od startu, odwiedzamy rekurencyjnie jego pierwszego nieodwiedzonego sąsiada itd., wracamy dopiero gdy nie ma gdzie pójść. DFS również tworzy drzewo przeszukiwania (a dokładniej *las*, jeśli graf nie jest spójny, bo możemy uruchomić DFS ponownie z kolejnego nieodwiedzonego wierzchołka). **Złożoność DFS wynosi $O(|V|+|E|)$**. Zastosowania DFS: wykrywanie cykli (np. *krawędź wsteczna* odkryta podczas DFS świadczy o istnieniu cyklu), topologiczne sortowanie DAG-ów (poprzez kolejność przetworzenia wierzchołków – patrz niżej), znajdowanie mostów i punktów artykulacji (na podstawie czasów odwiedzenia i low-link values), wyznaczanie silnych składowych (algorytm Tarjana używa jednego DFS, Kosaraju dwóch DFS) itd.

* **Sortowanie topologiczne:** dotyczy **acyklicznych** grafów skierowanych (DAG – Directed Acyclic Graph). Celem jest linearny porządek wierzchołków zgodny ze wszystkimi relacjami skierowanymi (jeśli istnieje łuk $u\to v$, to w uporządkowaniu $u$ ma być przed $v$). Taki porządek istnieje wtedy i tylko wtedy, gdy graf jest acykliczny. Można go znaleźć w czasie $O(|V|+|E|)$. Jedna metoda to wykonywanie DFS i zapisywanie wierzchołków w momencie *zakończenia* odwiedzenia (post-order) – kolejność malejąca względem tych czasów zakończenia daje sortowanie topologiczne. Inny algorytm (Kahna) używa wielokrotnego wybierania wierzchołków o stopniu wejściowym 0. Sortowanie topologiczne jest używane np. do planowania zadań, rozwiązywania zależności (kompilacja źródeł), czy rozpoznawania czy dany digraf zawiera cykl (jeśli nie da się go w pełni posortować).

**Minimalne drzewo rozpinające (MST):** dla grafu spójnego *ważonego* (z wagą na każdej krawędzi) często szukamy podzbioru krawędzi tworzących drzewo spinające o minimalnej sumie wag. Klasyczne algorytmy MST to:

* *Algorytm Kruskala:* sortuje wszystkie krawędzie grafu rosnąco po wagach i dodaje je kolejno do wyniku, **pomijając** te, które tworzyłyby cykl z już dodanymi. W praktyce sprawdzanie cyklu robi się przez strukturę *Union-Find* (złączeń i znajdowania przedstawiciela zbioru) – dołączamy krawędź jeśli łączy dwa drzewa (dwie różne komponenty bieżącego lasu). Algorytm kończy się gdy dodano $n-1$ krawędzi. Złożoność z sortowaniem $O(E\log E)$, dominowaną przez sortowanie (Union-Find działa praktycznie w czasie $O(E\alpha(V))\approx O(E)$). Kruskal dobrze sprawdza się przy rozproszonych grafach (mało wierzchołków, dużo krawędzi).
* *Algorytm Prima:* startuje z dowolnego wierzchołka i rozbudowuje drzewo: w każdym kroku dodaje **najtańszą** krawędź wychodzącą z już zbudowanego drzewa do nowego wierzchołka. Implementacja wykorzystuje kolejkę priorytetową trzymającą krawędzie kandydujące. Złożoność $O(E\log V)$ (bo przy każdym dodaniu wierzchołka aktualizujemy priorytety krawędzi wychodzących). W praktyce Prim bywa wydajniejszy dla gęstych grafów (dużo wierzchołków).

**Najkrótsze ścieżki w grafie:** to fundamentalny problem: znaleźć najkrótszą (minimalna waga lub liczba krawędzi) drogę między wybranymi wierzchołkami. Klasyczne algorytmy:

* *BFS* – już omawiany – znajdujący najkrótsze ścieżki w grafie **nieważonym** (lub o jednakowej wadze każdej krawędzi). Po wykonaniu BFS z źródła $s$ mamy odległość $d(s,v)$ dla każdego osiągalnego $v$ (w liczbie skoków).

* *Algorytm Dijkstry:* rozwiązuje problem najkrótszych ścieżek od źródła w grafie o **nieujemnych wagach**. Działa zachłannie podobnie do Prima: startuje z $s$, następnie iteracyjnie ustala najkrótszą odległość dla kolejnego wierzchołka (tego, do którego obecnie najtaniej dotrzeć) i *relaksuje* (aktualizuje) odległości sąsiadów tego wierzchołka. Implementacja z kopcem daje złożoność $O(E\log V)$. Jeżeli wagi są nieujemne, to w momencie zdejmowania wierzchołka z kolejki jego odległość jest finalna. Algorytm kończy po ustaleniu odległości do wszystkich wierzchołków (lub do zadanego celu).

* *Algorytm Bellmana-Forda:* również oblicza najkrótsze ścieżki z zadanej startowej $s$, **pozwala jednak na krawędzie o wagach ujemnych** (byle nie było cyklu o sumie ujemnej dostępnego z $s$ – w przeciwnym razie odległości mogą maleć w nieskończoność). Idea: wykonujemy $n-1$ rund *relaksacji* wszystkich krawędzi (prób poprawy $d(u)$ przez $d(v)+w(v,u)$ dla każdej krawędzi $v\to u$). Po $n-1$ iteracjach odległości są najkrótsze, a dodatkowa $n$-ta iteracja wykryłaby ewentualny cykl ujemny (jeśli coś da się jeszcze poprawić). Złożoność $O(V\cdot E)$, co jest wolniejsze od Dijkstry dla dużych grafów, ale działa w ogólniejszych przypadkach (może służyć np. do znalezienia cyklu o ujemnej sumie wag, jeśli istnieje).

* *Inne:* Warto wspomnieć, że problem najkrótszych ścieżek między *wszystkimi* parami wierzchołków rozwiązuje algorytm Floyda-Warshalla w czasie $O(V^3)$ albo np. wielokrotne odpalenie Dijkstry (gdy brak wag ujemnych) w $O(V\cdot E\log V)$. Istnieje także wiele wyspecjalizowanych algorytmów grafowych (znalezienie cyklu Eulera, cyklu Hamiltona – NP-trudne, znajdowanie skojarzeń, przepływy w sieciach, itp.), ale wykraczają one poza zakres tej notatki.




## Kolorowanie grafów

* **Kolorowanie wierzchołków:** przypisanie każdemu wierzchołkowi grafu pewnego koloru w taki sposób, by żadne dwa sąsiednie wierzchołki nie miały tego samego koloru. Minimalną liczbę kolorów potrzebną do prawidłowego pokolorowania wierzchołków grafu $G$ nazywamy **liczbą chromatyczną** $\chi(G)$. Jeśli $\chi(G)=k$, mówimy że graf jest *$k$-chromatyczny*. Przykłady: graf zerowy $N\_n$ (bez krawędzi) ma $\chi=1$, każdy graf dwudzielny niepusty $\chi=2$ (bo można dwoma kolorami pokolorować dwie strony), $K\_n$ ma $\chi = n$ (każdy wierzchołek musi otrzymać inny kolor), cykl parzysty $C\_{2m}$ jest 2-chromatyczny, a cykl nieparzysty $C\_{2m+1}$ – 3-chromatyczny (nie da się dwoma z powodu obecności nieparzystego cyklu). Nie istnieje prosty wzorzec dla grafów 3-chromatycznych – np. graf Petersena ma $\chi=3$ jako nietrywialny przykład.

* **Kolorowanie krawędzi:** analogicznie możemy kolorować krawędzie tak, aby żadne dwie krawędzie incydentne (spotykające się w jakimś wierzchołku) nie miały tego samego koloru. Minimalna liczba kolorów potrzebna na takie kolorowanie to **indeks chromatyczny** grafu, oznaczany zwykle $\chi'(G)$ lub $\chi\_0(G)$. Przykład: krawędzie $K\_5$ wymagają 5 kolorów, a $K\_4$ tylko 3 (w ogólności pełny graf $K\_n$ ma $\chi' = n$ dla n nieparzystego i $\chi' = n-1$ dla parzystego – to wynik związany z problemem klasztoru i ułamaniem kompletu na mecze)\*\*.

* **Twierdzenie o stopniach a kolorowaniu:** prosty, ale użyteczny fakt: dowolny graf $G$ można pokolorować wierzchołki w co najwyżej $\Delta(G)+1$ kolorach, gdzie $\Delta$ to maksymalny stopień wierzchołka. (Wystarczy użyć algorytmu zachłannego kolorowania, rozważając wierzchołki w pewnej kolejności – każdorazowo wolny jest co najmniej jeden kolor spośród $\Delta+1$). To ograniczenie można poprawić następująco: **twierdzenie Brooksa:** jeśli $G$ jest spójnym prostym grafem i nie jest kliką ($K\_n$) ani nieparzystym cyklem, a $\Delta(G)\ge 3$, to $\chi(G)\le \Delta(G)$. Innymi słowy, oprócz wyjątkowych przypadków kompletnych grafów i cykli, do pokolorowania grafu wystarczy tylu kolorów co wynosi maksymalny stopień. Przykładowo graf o strukturze gwiazdy $K\_{1,s}$ ma $\Delta = s$, ale $\chi=2$ (spełnia warunki Brooksa, bo nie jest kliką ani $C\_{2k+1}$).

* **Twierdzenie Vizinga:** dotyczy kolorowania **krawędzi**. Mówi ono, że **dla każdego prostego grafu $G$ indeks chromatyczny spełnia $\Delta(G) \le \chi'(G) \le \Delta(G)+1$**. Innymi słowy, do pokolorowania krawędzi nigdy nie potrzeba więcej niż $\Delta+1$ kolorów, a dość często wystarcza dokładnie $\Delta$. Grafy, dla których $\chi' = \Delta$, nazywa się *grafami klasy 1*, a te gdzie $\chi' = \Delta+1$ – *grafami klasy 2*. Przykładowo $K\_5$ jest klasy 2 (trzeba 5 kolorów na 4), ale graf dwudzielny $K\_{m,n}$ zawsze jest klasy 1 – według twierdzenia Königa (1916) każdemu grafowi dwudzielnemu można pokolorować krawędzie w $\Delta$ kolorach.

* **Kolorowanie map:** problem słynnego *kolorowania map* sprowadza się do kolorowania wierzchołków grafów planarnych (regiony na mapie reprezentuje się przez graf sąsiedztwa). Dla grafów planarnych obowiązują dodatkowe ograniczenia na $\chi$. Wiemy już, że w grafie planarnym musi istnieć wierzchołek stopnia $\le 5$ – na tej obserwacji opiera się **twierdzenie o 5 kolorach:** każdy prosty graf planarny da się pokolorować co najwyżej 5 kolorami. Dowód tego twierdzenia jest możliwy indukcją usuwając kolejno wierzchołki stopnia $\le 5$ i dodając z powrotem, dobierając dla nich pasujący kolor (jeśli w danej chwili wierzchołek ma pięciu sąsiadów o pięciu różnych kolorach, to jedna z par jego sąsiadów nie jest połączona krawędzią – zamiana kolorów u części z nich zwalnia kolor dla naszego wierzchołka). Natomiast **słynne twierdzenie o 4 kolorach** (Appel, Haken 1976) mówi, że **każdy graf planarny jest 4-kolorowalny**. Problem ten postawiono już w XIX wieku, jednak jego pełny dowód okazał się bardzo skomplikowany i był pierwszym dowodem matematycznym z istotnym użyciem komputera (sprawdzenie dużej liczby konfiguracji). Do dziś dowód 4-kolorowego twierdzenia jest przedmiotem zainteresowania (istnieją uproszczenia, lecz nadal bazują na sprawdzeniu komputerowym wielu przypadków).
