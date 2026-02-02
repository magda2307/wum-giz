# Notatki z NLP - Definicje i Pojęcia

## 1. Wstęp do NLP i Przetwarzanie Tekstu

* **[span_0](start_span)NLP (Natural Language Processing)** – Dziedzina łącząca sztuczną inteligencję (AI), uczenie maszynowe (ML) i głębokie uczenie (DL), zajmująca się przetwarzaniem języka ludzkiego[span_0](end_span).
* **[span_1](start_span)Fonemy** – Najmniejsze jednostki dźwięku (mowa i dźwięki)[span_1](end_span).
* **[span_2](start_span)[span_3](start_span)Morfemy i Leksemy** – Elementy składowe słów (rdzenie, przedrostki) oraz całe słowa[span_2](end_span)[span_3](end_span).
* **[span_4](start_span)[span_5](start_span)Składnia (Syntax)** – Struktura fraz i zdań (np. drzewa rozbioru gramatycznego)[span_4](end_span)[span_5](end_span).
* **[span_6](start_span)Niejednoznaczność (Ambiguity)** – Problem w NLP, gdzie zdania mogą być interpretowane na wiele sposobów (np. niejasne odniesienia zaimków)[span_6](end_span).
* **[span_7](start_span)Pipeline NLP** – Sekwencja kroków przetwarzania: zbieranie danych, czyszczenie, preprocessing, inżynieria cech, modelowanie, ewaluacja[span_7](end_span).
* **[span_8](start_span)Tokenizacja** – Proces podziału tekstu na mniejsze jednostki, takie jak słowa lub zdania (np. "Let's" -> "Let", "'s")[span_8](end_span).
* **[span_9](start_span)Stemming** – Mechaniczne obcinanie końcówek słów w celu sprowadzenia ich do rdzenia (np. "formality" -> "formaliti")[span_9](end_span).
* **[span_10](start_span)Lematyzacja** – Sprowadzanie słowa do jego formy podstawowej/słownikowej z uwzględnieniem kontekstu (np. "was" -> "be")[span_10](end_span).
* **[span_11](start_span)Normalizacja** – Ujednolicanie tekstu, np. zamiana na małe litery, usuwanie interpunkcji[span_11](end_span).
* **[span_12](start_span)POS Tagging (Part-of-Speech)** – Przypisywanie słowom kategorii gramatycznych (np. rzeczownik, czasownik)[span_12](end_span).
* **[span_13](start_span)Parsing** – Analiza struktury gramatycznej zdania (drzewa składniowe)[span_13](end_span).
* **[span_14](start_span)Coreference Resolution** – Identyfikacja, do jakiego bytu odnoszą się wyrażenia w tekście (np. przypisanie zaimka "his" do osoby wymienionej wcześniej)[span_14](end_span).
* **[span_15](start_span)Metryki ewaluacji** – Miary oceny modeli, m.in.: Accuracy, Precision/Recall/F1, BLEU, ROUGE, Perplexity[span_15](end_span).

---

## 2. Reprezentacja Wektorowa Tekstu (Embeddings)

* **[span_16](start_span)One-Hot Encoding** – Reprezentacja wektorowa, gdzie słowo to wektor zer z jedną jedynką; nie oddaje podobieństwa semantycznego[span_16](end_span).
* **[span_17](start_span)Bag of Words (BoW)** – Model reprezentujący tekst jako zbiór słów i ich liczności, ignorujący kolejność i gramatykę[span_17](end_span).
* **[span_18](start_span)N-Grams** – Ciągłe sekwencje $N$ tokenów (np. unigramy, bigramy), pozwalające zachować lokalny kontekst[span_18](end_span).
* **[span_19](start_span)TF-IDF** – Metoda ważenia słów: iloczyn częstości słowa w dokumencie (TF) i odwrotnej częstości w korpusie (IDF), co zmniejsza wagę słów pospolitych[span_19](end_span).
* **[span_20](start_span)Word Embeddings** – Gęste wektory w wielowymiarowej przestrzeni, które reprezentują znaczenie semantyczne (podobne słowa są blisko siebie)[span_20](end_span).
* **[span_21](start_span)Word2Vec** – Technika tworzenia embeddingów wykorzystująca sieci neuronowe[span_21](end_span). Wyróżnia dwa modele:
    * **[span_22](start_span)CBOW (Continuous Bag of Words)** – Przewiduje słowo środkowe na podstawie kontekstu[span_22](end_span).
    * **[span_23](start_span)Skip-gram** – Przewiduje słowa kontekstowe na podstawie słowa środkowego[span_23](end_span).
* **[span_24](start_span)GloVe & fastText** – Inne popularne modele pre-trenowanych embeddingów[span_24](end_span).
* **[span_25](start_span)t-SNE** – Algorytm redukcji wymiarowości używany do wizualizacji embeddingów w 2D/3D[span_25](end_span).

---

## 3. Teoria Transformerów

* **[span_26](start_span)Transformer** – Architektura sieci neuronowej oparta na mechanizmie uwagi, przetwarzająca całe sekwencje jednocześnie (bez rekurencji)[span_26](end_span).
* **[span_27](start_span)Mechanizm Attention** – Pozwala modelowi skupić się na różnych częściach wejścia podczas przetwarzania[span_27](end_span).
* **[span_28](start_span)Self-Attention** – Mechanizm, w którym słowa w zdaniu "patrzą" na inne słowa w tym samym zdaniu, by zrozumieć kontekst (np. powiązanie zaimka z podmiotem)[span_28](end_span).
* **[span_29](start_span)Multi-head Attention** – Zastosowanie wielu równoległych "głowic" uwagi, by model uczył się różnych relacji jednocześnie[span_29](end_span).
* **[span_30](start_span)Encoder** – Część kodująca wejście; przetwarza tekst na reprezentację wektorową (np. BERT)[span_30](end_span).
* **[span_31](start_span)Decoder** – Część generująca wyjście; tworzy tekst token po tokenie (np. GPT)[span_31](end_span).
* **[span_32](start_span)Autoencoding models (Encoder-only)** – Modele widzące kontekst dwukierunkowo (np. BERT, RoBERTa), używane do klasyfikacji i analizy tekstu[span_32](end_span).
* **[span_33](start_span)Autoregressive models (Decoder-only)** – Modele jednokierunkowe (np. GPT, CTRL), używane do generowania tekstu[span_33](end_span).
* **[span_34](start_span)Sequence-to-Sequence** – Modele z koderem i dekoderem (np. T5, BART), używane do tłumaczeń i streszczeń[span_34](end_span).
* **[span_35](start_span)Transfer Learning** – Trening wstępny (pre-training) na dużym korpusie, a następnie dostrajanie (fine-tuning) do konkretnego zadania[span_35](end_span).

---

## 4. Transformery w Praktyce

* **[span_36](start_span)HuggingFace Hub** – Centralne repozytorium modeli, zbiorów danych i metryk[span_36](end_span).
* **[span_37](start_span)Subword Tokenization** – Metoda podziału słów na podjednostki (np. "tokenizing" -> "token", "##izing"), obsługująca rzadkie słowa[span_37](end_span).
* **[span_38](start_span)Feature Extraction** – Wykorzystanie modelu z zamrożonymi wagami jako ekstraktora cech dla innego klasyfikatora[span_38](end_span).
* **[span_39](start_span)Fine-Tuning** – Trenowanie wszystkich parametrów modelu na nowym zbiorze danych (daje lepsze wyniki niż ekstrakcja cech)[span_39](end_span).
* **[span_40](start_span)Greedy Search** – Dekodowanie wybierające zawsze token o najwyższym prawdopodobieństwie (ryzyko powtórzeń)[span_40](end_span).
* **[span_41](start_span)Beam Search** – Dekodowanie śledzące kilka najbardziej prawdopodobnych ścieżek jednocześnie[span_41](end_span).
* **[span_42](start_span)Sampling** – Losowanie następnego tokena z rozkładu prawdopodobieństwa[span_42](end_span).
* **[span_43](start_span)Temperature** – Parametr skalujący logity przed softmaxem; niska temperatura zmniejsza losowość, wysoka zwiększa różnorodność[span_43](end_span).
* **[span_44](start_span)Top-k Sampling** – Ograniczenie losowania do $k$ najbardziej prawdopodobnych tokenów[span_44](end_span).
* **[span_45](start_span)Top-p (Nucleus) Sampling** – Ograniczenie losowania do zbioru tokenów, których suma prawdopodobieństw przekracza próg $p$[span_45](end_span).
