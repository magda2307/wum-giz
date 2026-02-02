# Notatki z NLP - Definicje i Pojęcia

## 1. Wstęp do NLP i Przetwarzanie Tekstu

* **NLP (Natural Language Processing)** – Dziedzina łącząca sztuczną inteligencję (AI), uczenie maszynowe (ML) i głębokie uczenie (DL), zajmująca się przetwarzaniem języka ludzkiego.
* **Fonemy** – Najmniejsze jednostki dźwięku w mowie.
* **Morfemy i Leksemy** – Elementy składowe słów (rdzenie, przedrostki) oraz całe słowa.
* **Składnia (Syntax)** – Struktura fraz i zdań (np. drzewa rozbioru gramatycznego).
* **Niejednoznaczność (Ambiguity)** – Problem w NLP, gdzie zdania mogą być interpretowane na wiele sposobów (np. niejasne odniesienia zaimków).
* **Pipeline NLP** – Sekwencja kroków przetwarzania: zbieranie danych, czyszczenie, preprocessing, inżynieria cech, modelowanie, ewaluacja.
* **Tokenizacja** – Proces podziału tekstu na mniejsze jednostki, takie jak słowa lub zdania.
* **Stemming** – Mechaniczne obcinanie końcówek słów w celu sprowadzenia ich do rdzenia (np. "formality" zmienia się w "formaliti").
* **Lematyzacja** – Sprowadzanie słowa do jego formy podstawowej lub słownikowej z uwzględnieniem kontekstu (np. "was" zmienia się w "be").
* **Normalizacja** – Ujednolicanie tekstu, np. zamiana na małe litery, usuwanie interpunkcji.
* **POS Tagging** – Przypisywanie słowom kategorii gramatycznych (np. rzeczownik, czasownik).
* **Parsing** – Analiza struktury gramatycznej zdania (tworzenie drzew składniowych).
* **Coreference Resolution** – Identyfikacja, do jakiego bytu odnoszą się wyrażenia w tekście (np. przypisanie zaimka "on" do osoby wymienionej wcześniej).
* **Metryki ewaluacji** – Miary oceny modeli, m.in.: Accuracy, Precision, Recall, F1, BLEU, ROUGE, Perplexity.

---

## 2. Reprezentacja Wektorowa Tekstu (Embeddings)

* **One-Hot Encoding** – Reprezentacja wektorowa, gdzie słowo to wektor zer z jedną jedynką; metoda ta nie oddaje podobieństwa znaczeniowego.
* **Bag of Words (BoW)** – Model reprezentujący tekst jako zbiór słów i ich liczności, ignorujący kolejność i gramatykę.
* **N-Grams** – Ciągłe sekwencje N tokenów (np. unigramy dla N=1, bigramy dla N=2), pozwalające zachować lokalny kontekst.
* **TF-IDF** – Metoda ważenia słów: iloczyn częstości słowa w dokumencie (TF) i odwrotnej częstości w korpusie (IDF), co zmniejsza wagę słów pospolitych.
* **Word Embeddings** – Gęste wektory w wielowymiarowej przestrzeni, które reprezentują znaczenie semantyczne (słowa o podobnym znaczeniu są blisko siebie).
* **Word2Vec** – Technika tworzenia embeddingów wykorzystująca sieci neuronowe. Wyróżnia dwa modele:
    * **CBOW** – Przewiduje słowo środkowe na podstawie kontekstu.
    * **Skip-gram** – Przewiduje słowa kontekstowe na podstawie słowa środkowego.
* **GloVe i fastText** – Inne popularne modele pre-trenowanych embeddingów.
* **t-SNE** – Algorytm redukcji wymiarowości używany do wizualizacji embeddingów na płaszczyźnie 2D lub 3D.

---

## 3. Teoria Transformerów

* **Transformer** – Architektura sieci neuronowej oparta na mechanizmie uwagi, przetwarzająca całe sekwencje jednocześnie (bez rekurencji).
* **Mechanizm Attention** – Pozwala modelowi skupić się na różnych częściach wejścia podczas przetwarzania.
* **Self-Attention** – Mechanizm, w którym słowa w zdaniu analizują relacje z innymi słowami w tym samym zdaniu, by zrozumieć kontekst.
* **Multi-head Attention** – Zastosowanie wielu równoległych głowic uwagi, by model uczył się różnych relacji jednocześnie.
* **Encoder** – Część kodująca wejście; przetwarza tekst na reprezentację liczbową (np. BERT).
* **Decoder** – Część generująca wyjście; tworzy tekst słowo po słowie (np. GPT).
* **Autoencoding models (Encoder-only)** – Modele widzące kontekst dwukierunkowo (np. BERT, RoBERTa), używane do klasyfikacji.
* **Autoregressive models (Decoder-only)** – Modele jednokierunkowe (np. GPT), używane do generowania tekstu.
* **Sequence-to-Sequence** – Modele z koderem i dekoderem (np. T5, BART), używane do tłumaczeń.
* **Transfer Learning** – Trening wstępny na dużym korpusie danych, a następnie dostrajanie (fine-tuning) do konkretnego zadania.

---

## 4. Transformery w Praktyce

* **HuggingFace Hub** – Centralne repozytorium modeli, zbiorów danych i narzędzi.
* **Subword Tokenization** – Metoda podziału słów na podjednostki (np. "tokenizing" na "token" i końcówkę "izing"), obsługująca rzadkie słowa.
* **Feature Extraction** – Wykorzystanie modelu z zamrożonymi wagami jako źródła cech dla innego klasyfikatora.
* **Fine-Tuning** – Trenowanie wszystkich parametrów modelu na nowym zbiorze danych (daje lepsze wyniki niż ekstrakcja cech).
* **Greedy Search** – Metoda generowania tekstu wybierająca zawsze słowo o najwyższym prawdopodobieństwie.
* **Beam Search** – Metoda śledząca kilka najbardziej prawdopodobnych ścieżek generowania tekstu jednocześnie.
* **Sampling** – Losowanie następnego słowa z rozkładu prawdopodobieństwa.
* **Temperature** – Parametr kontrolujący losowość; niska temperatura zmniejsza różnorodność, wysoka ją zwiększa.
* **Top-k Sampling** – Ograniczenie losowania do k najbardziej prawdopodobnych słów.
* **Top-p (Nucleus) Sampling** – Ograniczenie losowania do zbioru słów, których suma prawdopodobieństw przekracza próg p.
