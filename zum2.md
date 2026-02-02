# ZUM — NLP (Applied Machine Learning) — notatki do egzaminu

> Opracowanie na podstawie slajdów z wykładów ZUM (NLP) — Dominika Wnuk.  
> Zakres: Wykład 1 (wstęp), NLP_02 (wektoryzacja), NLP_03 (advanced language modelling), NLP_04 (Transformers in practice).  
> Data opracowania: 2026-02-02

---

## Jak się uczyć z tych notatek (1–2h przed egzaminem)

1. **Najpierw definicje i różnice**: BoW vs TF‑IDF vs embeddingi; encoder-only vs decoder-only vs seq2seq; greedy vs beam vs sampling.
2. **Potem „dlaczego”**: co psuje dane w preprocessingu, czemu TF‑IDF działa lepiej niż gołe zliczenia, czemu attention „widzi” kontekst.
3. **Na końcu**: typowe pytania egzaminacyjne (sekcje „Pytania” w każdym rozdziale).

---

# Wykład 1 — Wprowadzenie do NLP

## 1) Czym jest NLP i po co?

- **NLP (Natural Language Processing)**: metody i systemy do analizy/generowania języka naturalnego.
- Język to nie tylko słowa: zawiera **kulturę, kontekst, wiedzę o świecie**.

### Typowe zadania NLP
- **Language modeling** (modelowanie języka / generacja)
- **Text classification** (np. sentiment, temat, spam)
- **Information extraction** (np. NER — rozpoznawanie encji)
- **Information retrieval** (wyszukiwanie)
- **Conversational agent** (chatbot)
- **Summarization** (streszczenia)
- **Question answering**
- **Machine translation**
- **Topic modeling**

## 2) Składniki języka (co modelujemy)

- **Fonemy** (phonemes) — dźwięki.
- **Morfemy i leksemy** — „najmniejsze znaczące elementy” i jednostki słownikowe.
- **Składnia (syntax)** — struktura zdania.
- **Semantyka vs pragmatyka**:
  - *semantics*: znaczenie „dosłowne”
  - *pragmatics*: znaczenie w kontekście, intencje, implikacje

## 3) NLP jest trudne, bo…

### Ambiguity (wieloznaczność)
- To samo zdanie może mieć różne interpretacje (sens zależy od kontekstu).

### Common knowledge (wiedza o świecie)
- „a man bit a dog” vs „a dog bit a man” — oba poprawne gramatycznie, ale jedno jest „bardziej prawdopodobne” dla człowieka.

### Language diversity (różnorodność języków)
- Brak 1:1 mapowania między językami (*lack of equivalence*).
- Systemy **language-agnostic** vs **language-specific**.

### Inne wyzwania
- **high-resource vs low-resource** języki (ilość danych),
- **morphologically rich** (bogata fleksja),
- duża wariancja słownictwa,
- języki **CJK** (Chinese/Japanese/Korean) — tokenizacja i segmentacja.

## 4) Podejścia do NLP (historycznie i praktycznie)

- **Heurystyczne**: reguły, słowniki.
- **ML**: Naive Bayes, SVM, HMM, CRF.
- **DL**: RNN, LSTM, CNN, **Transformer** (obecnie dominujący w SOTA).

## 5) Pipeline NLP (od danych do modelu)

### 5.1 Data acquisition (pozyskanie danych)
- publiczne dane, scraping, generowanie danych („product invention”),
- **data augmentation**: synonym replacement, backtranslation, TF‑IDF-based replacement, bigram flipping, entity replacement, noise.

### 5.2 Text cleaning (czyszczenie)
- unicode normalization, korekta pisowni, system-specific error correction,
- deduplikacja,
- cleanup HTML / parsing.

### 5.3 Pre-processing (preprocessing)
- **Podstawy**: sentence segmentation, tokenization.
- **Częste kroki**: stopwords removal, stemming, lemmatization, usuwanie cyfr/punktuacji, lowercasing.
- **Inne**: normalisation, language detection, code mixing, transliteration.
- **Zaawansowane**: POS tagging, parsing, coreference resolution.

### 5.4 Feature engineering → Modeling → Evaluation
- Feature engineering (ręczne cechy / reprezentacje).
- Modeling: heurystyki → plan modelu → budowa i ulepszanie (ensemble/stacking, lepsze cechy, transfer learning, reapplication of heuristics).
- **Evaluation**: Accuracy, Precision/Recall/F1, AUC, MRR, MAP, BLEU, METEOR, ROUGE, Perplexity.

### Pytania, które lubią się pojawić (Wykład 1)
1. Wymień typowe zadania NLP i przykładowe zastosowania.
2. Co to jest semantyka vs pragmatyka?
3. Na czym polega preprocessing i które kroki są „częste”, a które „zaawansowane”?
4. Podaj przykłady data augmentation dla tekstu.
5. Jak dobrać metrykę do zadania (np. BLEU/ROUGE/perplexity)?

---

# NLP_02 — Vectorized Word Representations (wektoryzacja tekstu)

## 1) Po co wektory?
Modele ML/DL nie rozumieją tekstu „jako tekst” — potrzebują **liczb**. Wektoryzacja mapuje tekst → przestrzeń liczb (Vector Space Model).

## 2) Klasyczne reprezentacje

### 2.1 One-hot encoding
- Słownik V o rozmiarze |V|.
- Każde słowo → wektor długości |V| z jedną „1” na pozycji słowa.
- Plusy: proste.
- Minusy:
  - bardzo wysokowymiarowe i rzadkie (sparse),
  - **nie ma semantycznej bliskości** (dog i cat są tak samo „daleko” jak dog i airplane).

### 2.2 Bag of Words (BoW)
- Dokument → wektor zliczeń słów z vocab.
- Ignoruje kolejność słów.

**Przykład** (vocab: the, cat, sat, in, hat, with):
- „the cat sat” → [1,1,1,0,0,0]
- „the cat sat in the hat” → [2,1,1,1,1,0]

### 2.3 N-grams
- **n-gram**: ciąg n kolejnych tokenów (np. bigramy, trigramy).
- Bag of n-grams częściowo łapie kolejność („nie” + „lubię” ≠ „lubię” + „nie”).

### 2.4 TF‑IDF (ważenie słów)
Cel: słowa częste w dokumencie, ale rzadkie w korpusie, są bardziej informacyjne.

- **TF(t,d)** = (liczba wystąpień termu t w dokumencie d) / (liczba wszystkich termów w d)
- **IDF(t)** = log( N / df(t) ), gdzie:
  - N = liczba dokumentów w korpusie,
  - df(t) = liczba dokumentów zawierających t.
- **TF‑IDF(t,d)** = TF(t,d) * IDF(t)

**Intuicja**:
- „the” ma wysokie TF, ale też wysokie df → niskie IDF → niska waga.
- słowo domenowe (np. „cholesterol” w medycynie) ma zwykle wyższe IDF.

## 3) Reprezentacje rozproszone (Distributed representations)

### 3.1 Dystrybucyjna hipoteza (distributional hypothesis)
„Słowa o podobnym znaczeniu pojawiają się w podobnych kontekstach.”

Stąd:
- **embedding** = gęsty wektor (np. 300D) uczony tak, by podobne konteksty → podobne wektory.

### 3.2 Word embeddings
- Zjawisko analogii: **King – Man + Woman ≈ Queen** (przykład „semantyki wektorowej”).

### 3.3 Pre-trained embeddings
- **GloVe**, **word2vec**, **fastText** (często używane gotowce).

## 4) Trenowanie własnych embeddingów

### 4.1 CBOW (Continuous Bag of Words)
- Wejście: kontekst (słowa wokół)
- Wyjście: przewidywane słowo centralne (target)

Przykład na „The quick brown fox jumped over the lazy dog”:
- (context=(quick,brown), target=the), itd.

### 4.2 Skip-gram
- Wejście: słowo centralne (target)
- Wyjście: słowa kontekstu

**Różnica** (często pytana):
- CBOW: kontekst → target (dobry, gdy dużo danych i chcemy szybciej)
- Skip-gram: target → kontekst (często lepszy dla rzadkich słów)

### 4.3 Hiperparametry embeddingów
- **Wymiar wektora** (np. 100/300/768…)
- **Okno kontekstu** (context window)

## 5) Dalej niż słowa
- embeddingi dla subwordów/znaków, dokumentów.
- **Contextual representations**: wektory zależne od kontekstu zdania (transformery/LLM).

## 6) Wizualizacja embeddingów
- t‑SNE / PCA do rzutowania na 2D (analiza jakości przestrzeni).

### Pytania egzaminacyjne (NLP_02)
1. One-hot vs BoW vs TF‑IDF — porównaj + wady/zalety.
2. Dlaczego TF‑IDF „działa” lepiej niż zliczenia w wielu klasyfikacjach?
3. Co mówi distributional hypothesis?
4. CBOW vs skip-gram — czym się różnią (kierunek predykcji) i kiedy które?
5. Co to jest embedding i czemu jest „dense”?

---

# NLP_03 — Advanced Language Modelling (Transformery, GPT, BERT)

## 1) Encoder–decoder (seq2seq) — klasyczny schemat
- **Encoder** koduje sekwencję wejściową do reprezentacji ukrytej.
- **Decoder** generuje sekwencję wyjściową na podstawie tej reprezentacji (i poprzednich tokenów).

## 2) Attention (uwaga)
Idea: zamiast „ściskać” całe zdanie w jeden wektor, model uczy się **ważyć** elementy wejścia pod konkretne kroki wyjścia.

### Scaled dot‑product attention (rdzeń transformera)
- wejścia: **Q** (queries), **K** (keys), **V** (values)
- waga podobieństwa: Q·Kᵀ
- „scaled”: dzielenie przez √dₖ stabilizuje gradienty
- softmax → rozkład wag
- wynik: softmax(QKᵀ / √dₖ) V

### Multi-head attention
- Zamiast jednego attention, kilka „głów”, które uczą się różnych relacji (składnia, coreference, zależności długodystansowe…).

## 3) Transfer learning w NLP
- Pretraining na dużym korpusie → adaptacja do zadania docelowego.

### ULMFiT (przykład transfer learningu)
- **Pretraining**
- **Domain adaptation**
- **Fine-tuning**

## 4) Transformer — architektura (co trzeba umieć opowiedzieć)

### 4.1 Encoder
- blok: multi-head self-attention → feed-forward → residual connections + layer norm
- **Self-attention**: tokeny „patrzą” na siebie w obrębie tej samej sekwencji.

### 4.2 Positional embeddings
Transformery nie mają „wbudowanej kolejności”, więc dodajemy informacje o pozycji:
- **absolute positional representations**
- **relative positional representations**

### 4.3 Decoder
- podobny do encodera, ale z:
  - **masked self-attention** (żeby nie „podglądać” przyszłych tokenów),
  - attention na wyjściu encodera (w seq2seq).

## 5) Typy modeli transformerowych (klasyfikacja z HuggingFace)
- **Decoder-only (autoregressive)**: GPT, CTRL, Transformer‑XL, XLNet, …
- **Encoder-only (autoencoding)**: BERT, RoBERTa, DistilBERT, ALBERT, XLM, ELECTRA, Longformer, …
- **Seq2seq (encoder–decoder)**: T5, BART, Pegasus, …
- Inne: multimodal, retrieval-based itd.

## 6) GPT (modele generatywne, autoregresywne)
- GPT‑1 (2018), GPT‑2 (2019), GPT‑3 (2020), GPT‑4 (2023) — kolejne skalowania modeli.
- Typowe osiągnięcia: unsupervised pretraining, task conditioning, few/zero-shot, in-context learning.

## 7) BERT (encoder-only)
- Pretraining:
  - **MLM** (masked language modeling)
  - **NSP** (next sentence prediction)
- Fine-tuning: dokładamy „głowę” do konkretnego zadania (klasyfikacja, QA, NER).

### 7.1 Warianty BERT
- ALBERT, RoBERTa (m.in. bez NSP), DistilBERT (distillation), XLM (cross-lingual), ELECTRA (2 modele jak GAN), Longformer (długie sekwencje) itd.
- Kategorie wariantów: social LMs, monolingual, multilingual, domain-specific (FinBERT, SciBERT…), compact, character-based, efficient, long-sequence.

## 8) Wyzwania transformerów
- język i jego złożoność,
- dostępność danych,
- długie dokumenty,
- opacity (trudna interpretacja),
- bias.

### Pytania egzaminacyjne (NLP_03)
1. Co to jest encoder–decoder i gdzie się go używa?
2. Wyjaśnij attention (Q/K/V) i czemu jest „scaled”.
3. Multi-head attention — po co wiele głów?
4. Encoder-only vs decoder-only vs seq2seq — przykłady modeli + zastosowania.
5. Jak BERT jest trenowany (MLM, NSP) i jak go fine-tunować?
6. Jak działa transfer learning w NLP (pretrain → adapt → fine-tune)?

---

# NLP_04 — Transformers in practice (HuggingFace, klasyfikacja i generacja)

## 1) HF pipeline i praca z datasetami
- W praktyce często startuje się od:
  - `datasets` (HF datasets) + `transformers` (modele i tokenizery),
  - pipeline do szybkiego prototypowania.

## 2) Tokenizacja subword (ważne na egzamin)
- Modele nie działają na „czystych słowach”, tylko na tokenach (często subword).
- Zalety subword:
  - radzi sobie z OOV (out-of-vocabulary),
  - lepsze dla fleksji i nazw własnych.

## 3) Transformers jako feature extractor (bez fine-tuningu)
Pomysł:
1. bierzemy pre-trained model,
2. przepuszczamy tekst,
3. wyciągamy **ostatnie hidden states** (np. 768D),
4. budujemy macierz cech X i uczymy prosty klasyfikator (np. logistic regression).

### Kodowo (schemat)
- macierz: `X_train.shape == (n_samples, hidden_dim)` np. (16008, 768)
- baseline:
  - **DummyClassifier (most frequent)** — punkt odniesienia,
  - logistic regression na hidden states.

## 4) Fine-tuning transformera do klasyfikacji
- Przy fine-tuningu **wszystkie parametry** modelu są trenowalne (gradienty idą przez całość).
- Ustalasz:
  - model (np. DistilBERT),
  - tokenizację całego datasetu,
  - metryki: accuracy + weighted F1,
  - training args (batch size, lr, epochs),
  - trener (Trainer) i trening.

## 5) Error analysis
- Patrzysz na przypadki z największym loss / błędami.
- Cele:
  - znaleźć pattern (np. ironia, negacje, krótkie teksty),
  - sprawdzić jakość etykiet (label noise).

## 6) Saving + sharing (Hub)
- `trainer.push_to_hub(...)`
- potem można odpalić `pipeline` wskazując `model_id`.

---

## 7) Text generation (GPT‑2 / modele autoregresywne)

### 7.1 Greedy decoding
- W każdym kroku wybierasz token o max prawdopodobieństwie.
- Wada: łatwo wpada w monotonne/„głupie” generacje (lokalne maksimum, brak różnorodności).

### 7.2 Beam search
- Trzymasz **B** najlepszych częściowych sekwencji (beams) i rozwijasz je równolegle.
- Lepsze „globalnie” niż greedy, ale może produkować tekst zbyt „bezpieczny” / powtarzalny.

### 7.3 Sampling methods
Zamiast brać argmax, losujesz z rozkładu prawdopodobieństwa tokenów.

#### Temperature (T)
- softmax z temperaturą:
  - mniejsze **T** → rozkład ostrzejszy (mniej losowo, „chłodniej”)
  - większe **T** → bardziej płasko (więcej ryzyka i kreatywności)

#### Top-k sampling
- losujesz tylko z **k** najbardziej prawdopodobnych tokenów.

#### Nucleus sampling (top-p)
- losujesz z najmniejszego zbioru tokenów, którego łączna masa prawdopodobieństwa ≥ p (np. 0.9/0.95).

**Top-k vs top-p** (częste pytanie):
- top-k: stała liczba tokenów,
- top-p: zmienna liczba tokenów zależna od „pewności” modelu.

### Pytania egzaminacyjne (NLP_04)
1. Czym jest subword tokenization i czemu ją stosujemy?
2. Feature extractor vs fine-tuning — różnice, plusy/minusy.
3. Po co baseline (DummyClassifier)?
4. Jakie metryki dla klasyfikacji (accuracy + weighted F1) i czemu „weighted”?
5. Greedy vs beam vs sampling — kiedy które?
6. Co robi temperature / top-k / top-p?

---

# Szybka ściąga (najważniejsze różnice)

## BoW vs TF‑IDF vs embedding
- BoW: zlicza; brak ważenia; brak semantyki.
- TF‑IDF: zlicza + waży „informatywność” (rzadkie w korpusie, częste w dokumencie).
- Embedding: gęsty wektor uczony na kontekście (semantyczne podobieństwo).

## Encoder-only vs Decoder-only vs Seq2seq
- Encoder-only (BERT): „rozumienie” tekstu (klasyfikacja, NER, QA).
- Decoder-only (GPT): generacja (LM).
- Seq2seq (T5/BART): tłumaczenie, streszczenia, generacja warunkowa.

## Greedy vs Beam vs Sampling
- Greedy: najszybszy, ale monotonia.
- Beam: lepsza optymalizacja sekwencji, mniej różnorodny.
- Sampling: różnorodność; kontrola temperaturą/top-k/top-p.

---

## Checklist dzień przed
- Umiesz napisać wzór TF‑IDF i powiedzieć, co oznacza N/df.
- Umiesz powiedzieć, czym jest self-attention (Q/K/V) i po co multi-head.
- Umiesz rozróżnić: BERT vs GPT (cel treningu + kierunek).
- Umiesz wyjaśnić: fine-tuning vs feature extraction.
- Umiesz wytłumaczyć: temperature vs top-k vs nucleus sampling.
