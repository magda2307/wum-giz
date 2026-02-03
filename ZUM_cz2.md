# ZUM (Applied Machine Learning) — Notatki cz. 2  
**Zakres:** Computer Vision (fundamentals + detection/segmentation + generative), ASR (1–2), Multimodal LLMs  
*(opracowanie pod egzamin — definicje, porównania, typowe pytania)*

---

## Spis treści
1. [Computer Vision — fundamenty](#1-computer-vision--fundamenty)  
2. [Detection, Segmentation i Generative Models (Stable Diffusion)](#2-detection-segmentation-i-generative-models-stable-diffusion)  
3. [ASR 1 — podstawy sygnału audio i reprezentacji](#3-asr-1--podstawy-sygnału-audio-i-reprezentacji)  
4. [ASR 2 — modele rozpoznawania mowy i metryki](#4-asr-2--modele-rozpoznawania-mowy-i-metryki)  
5. [Multimodal LLMs](#5-multimodal-llms)  

---

## 1. Computer Vision — fundamenty

### 1.1. Co to jest Computer Vision (CV)?
**Computer Vision** = rozumienie danych wizualnych (obraz/wideo) przez modele ML/DL: od pikseli → do reprezentacji semantycznej (co jest na obrazie, gdzie, w jakiej formie).  
**Core tasks (trzon egzaminu):**
- **Image classification**: *jedna etykieta na cały obraz*.
- **Object detection**: *wiele obiektów + lokalizacja (bounding boxy)*.
- **Segmentation**: *klasyfikacja piksel po pikselu* (maska).  

**Największe wyzwanie:** **generalizacja** do zmienności świata realnego (inne oświetlenie, tło, kąty, rozdzielczość, szum, urządzenia).

---

### 1.2. Reprezentacja obrazu
**Obraz** = macierz wartości pikseli (np. `H x W x C`).  
**Przestrzenie barw:**
- **RGB** — 3 kanały (R,G,B).
- **HSV** — barwa/nasycenie/jasność (często wygodne w klasycznych metodach).
- **Grayscale** — 1 kanał (np. do detekcji krawędzi / klasycznych filtrów).

**Uwaga praktyczna (częsty haczyk):**
- kolejność kanałów bywa inna w bibliotekach: **Pillow** zwykle **RGB**, a **OpenCV** często **BGR**.

**Normalizacja / skalowanie**:
- modele zwykle oczekują wejścia o ustalonym zakresie (np. 0–1) i/lub standaryzacji (np. odjęcie średniej, podział przez odchylenie).  
Cel: stabilniejsze uczenie i porównywalna skala cech.

---

### 1.3. Preprocessing vs Augmentation
**Preprocessing** (deterministycznie):
- resize, crop, normalizacja.

**Data augmentation** (losowo):
- rotacje, flipy, zmiany jasności/kontrastu/koloru, szum, wycinanie fragmentów itd.  
Cel: **większa odporność** i **mniejszy overfitting**.

---

### 1.4. Klasyczne CV (przed deep learningiem)
**Edge detection (krawędzie):**
- Sobel (gradient),
- Canny (popularny detektor krawędzi).

**Feature extraction (cechy ręcznie projektowane):**
- **SIFT**,
- **HOG**.

**Klasyczna segmentacja:**
- progowanie (thresholding),
- watershed.

**Limitacje:** cechy „handcrafted” są często **wąsko domenowe** i gorzej generalizują; trudniej skalować do wielu scen.

---

### 1.5. Deep Learning w CV (CNN)
**CNN** automatycznie uczy się hierarchii cech:
- niskopoziomowe (krawędzie, tekstury),
- wyższopoziomowe (części obiektów),
- semantyka (całe obiekty).

**Typowy pipeline w CNN:**
1. **Convolutional layer** — ekstrakcja cech.
2. **Pooling** — downsampling (zmniejsza wymiar, zwiększa odporność).
3. **Activation** (np. ReLU) — nieliniowość.
4. **Fully connected** — klasyfikacja.

**Dlaczego DL wygrał?** Skaluje się z dużymi danymi (np. ImageNet) i GPU; lepsza dokładność/robustness.

---

### 1.6. Popularne architektury CNN (warto znać „co po czym”)
- **LeNet (1998)** — klasyka, cyfry.
- **AlexNet (2012)** — przełom na ImageNet (start boomu DL w CV).
- **VGG (2014)** — „prosta” głęboka architektura.
- **ResNet (2015)** — skip connections (łatwiej trenować bardzo głębokie sieci).

---

### 1.7. Transfer learning
**Idea:** używasz modelu pre-trained (np. ResNet/EfficientNet) jako ekstraktora cech i dopasowujesz do swojego problemu.  
**Dwa podejścia:**
- **freeze lower layers** (zamrażasz wczesne warstwy), uczysz głównie „głowę” klasyfikacyjną,
- **fine-tuning** — odblokowujesz część warstw i dostrajasz.

**Plusy:** mniej danych, szybsza konwergencja.

---

### 1.8. Pipeline trenowania i metryki
**Kroki:**
1. dataset (np. CIFAR-10/ImageNet),
2. preprocessing + augmentation,
3. train/validate,
4. ewaluacja.

**Metryki** (podstawy):
- **accuracy** (częściej w klasyfikacji),
- **precision/recall** (ważne przy niezbalansowanych klasach),
- **IoU** (Intersection-over-Union) — kluczowe w detekcji/segmentacji.

---

### 1.9. Typowe pytania egzaminacyjne (CV fundamentals)
- *Czym różni się preprocessing od augmentation? Podaj przykłady.*
- *Dlaczego potrzebujemy normalizacji wejścia do modelu?*
- *Co daje transfer learning i kiedy ma sens?*
- *Co to jest IoU i do czego służy?*
- *Dlaczego ResNet (skip connections) umożliwia trenowanie głębszych sieci?*

---

## 2. Detection, Segmentation i Generative Models (Stable Diffusion)

### 2.1. Od klasyfikacji do detekcji i segmentacji
- **Classification**: „co jest na obrazku?”
- **Detection**: „co i gdzie?”
- **Segmentation**: „które piksele należą do czego?”

Wraz z przejściem w prawo rośnie precyzja i złożoność.

---

### 2.2. Object detection — podstawy
**Cel:** zidentyfikować obiekty + ich lokalizacje.  
**Reprezentacja wyjścia:** **bounding boxy + etykiety klas**.

**Ewolucja podejścia:**
- sliding windows (historycznie) →  
- region proposals →  
- end-to-end (współcześnie, single-shot / transformerowe).

**Datasety (warto kojarzyć nazwy):** COCO, Pascal VOC.

---

### 2.3. Modele detekcji: rodziny i trade-off
**Rodziny:**
- **R-CNN → Fast R-CNN → Faster R-CNN** (region-based; zwykle dokładniejsze, wolniejsze),
- **YOLO (You Only Look Once)** — single-shot, real-time,
- **SSD (Single Shot Multibox Detector)** — kompromis szybkość vs jakość.

**Trade-off:** **precision vs inference time** (dokładność vs czas predykcji).

---

### 2.4. Segmentacja: semantic vs instance
- **Semantic segmentation**: każdy piksel dostaje klasę (np. „osoba”).
- **Instance segmentation**: rozdziela *konkretne instancje* tej samej klasy (osoba1, osoba2…).

**Największy problem praktyczny:** utrzymanie granic obiektów (object boundaries).

---

### 2.5. U-Net i Mask R-CNN
**U-Net**:
- encoder–decoder,
- **skip connections** → zachowanie detali przestrzennych,
- częsty w medycynie, mapach, robotyce.

**Mask R-CNN**:
- Faster R-CNN + dodatkowa „głowa” do maski segmentacji.

---

### 2.6. Generative models — po co i jakie?
**Cel:** nauczyć się rozkładu danych i generować nowe próbki.  
**Typy (minimum do zapamiętania):**
- **GAN**,
- **VAE**,
- **Diffusion models**.

**Zastosowania:**
- generowanie obrazów (sztuka),
- augmentacja danych,
- super-resolution.

---

### 2.7. GAN — intuicja i problemy
- **Generator** tworzy próbki „fake”.
- **Discriminator** odróżnia real vs fake.
- Uczenie = gra min–max (adversarial training).

**Typowe problemy:**
- **mode collapse** (generator produkuje mało zróżnicowane próbki),
- niestabilna konwergencja.

---

### 2.8. Diffusion models — intuicja
**Idea:** stopniowo dodajesz szum do obrazu (forward), a model uczy się proces odwracać (reverse: odszumianie).  
Efekt: stabilna, wysoka jakość generacji.

---

### 2.9. Stable Diffusion — architektura (to trzeba umieć opowiedzieć)
**Stable Diffusion** to **Latent Diffusion Model (LDM)**, czyli dyfuzja nie w pikselach, tylko w **przestrzeni latent**.

**Komponenty:**
- **Autoencoder**: kompresuje obraz do latent space i dekoduje z powrotem,
- **U-Net**: sieć odszumiająca w latent space,
- **CLIP text encoder**: zamienia prompt na embeddingi.

**Dlaczego latent?** Taniej obliczeniowo (mniejszy wymiar) przy zachowaniu jakości.

---

### 2.10. Prompt-to-Image (pipeline)
Text → embedding → latent noise → iteracyjne denoising (U-Net) → decode (autoencoder) → obraz.

**Sterowanie wynikiem:**
- **seed**: powtarzalność / różnorodność przy tym samym prompt,
- „strength” / „guidance” (zależnie od implementacji): jak mocno prompt prowadzi generację.

---

### 2.11. Fine-tuning i kontrola
- **DreamBooth**: personalizacja na kilku obrazach.
- **LoRA (Low-Rank Adaptation)**: lekkie dostrajanie (mało parametrów).
- **ControlNet**: warunkowanie generacji dodatkową informacją (pose, depth, edges).

---

### 2.12. „Co dalej” + etyka
**Trend:** foundation models w CV (np. CLIP, DINOv2, SAM) + vision-language (np. BLIP, Flamingo, GPT-4V) + multimodalność (text+image+video).  
**Ryzyka:**
- deepfakes/misinformation,
- bias w danych,
- copyright/ownership,
- potrzeba transparentności i odpowiedzialności.

---

### 2.13. Typowe pytania egzaminacyjne (Detection/Seg/Gen)
- *Semantic vs instance segmentation — definicja i przykład.*
- *Porównaj YOLO vs Faster R-CNN (szybkość i dokładność).*
- *Co to jest IoU i jak go używa się w detekcji?*
- *Dlaczego diffusion bywa „stabilniejsze” niż GAN?*
- *Wyjaśnij, co oznacza „latent diffusion” i po co autoencoder.*
- *Mode collapse — co to jest i dlaczego jest problemem?*
- *DreamBooth vs LoRA vs ControlNet — do czego służą?*

---

## 3. ASR 1 — podstawy sygnału audio i reprezentacji

### 3.1. Use cases ASR / audio
- dyktowanie,
- chatboty/asystenci głosowi,
- smart home,
- infolinie (automaty),
- transkrypcje (np. napisy),
- wyszukiwanie informacji,
- analiza korpusów.

---

### 3.2. Sygnał cyfrowy: sampling rate i bit depth
**Sampling rate (częstotliwość próbkowania)**: ile próbek na sekundę (Hz).  
- większy sampling rate → lepsze odwzorowanie wysokich częstotliwości, większy rozmiar danych.
- (intuicja egzaminacyjna) zbyt mały sampling → utrata informacji, aliasing.

**Bit depth (głębia bitowa)**: ile bitów na próbkę (precyzja amplitudy).  
- większy bit depth → mniejszy błąd kwantyzacji, większa dynamika, większy rozmiar.

---

### 3.3. Waveform, spectrum, spectrogram
- **Waveform**: amplituda w czasie (najbardziej „surowy” widok).
- **Spectrum**: amplituda vs częstotliwość (po FFT).
- **Spectrogram**: czas–częstotliwość (zwykle STFT), pokazuje jak składowe częstotliwości zmieniają się w czasie.

**Mel spectrogram**:
- skala mel lepiej odpowiada percepcji ludzkiego słuchu (zagęszczenie w niższych pasmach),
- częsty input do modeli (zwłaszcza klasyfikacja/ASR w pipeline z cechami).

---

### 3.4. Eksploracja audio (praktyka)
Typowy workflow (np. w librosa):
- wczytanie fali (`array`) + `sampling_rate`,
- wizualizacja `waveshow`,
- analiza cech (spectrogram/mel-spectrogram).

---

### 3.5. Preprocessing audio (w praktyce i na egzamin)
- **resampling** (ujednolicenie próbkowania),
- **filtrowanie datasetu** (np. zbyt krótkie/zepsute próbki),
- **konwersja audio → input modelu** (spectrogramy / cechy / waveform zależnie od modelu).

---

### 3.6. Streaming mode (datasets)
W dużych zbiorach (np. HF datasets) można ładować dane w trybie streaming — iterujesz po próbkach bez pobierania całości lokalnie.

---

### 3.7. Audio applications (szerszy kontekst)
- audio classification,
- ASR,
- speaker diarization / speaker identification,
- text-to-speech,
- keyword spotting / spoken term detection.

---

### 3.8. Typowe pytania egzaminacyjne (ASR 1)
- *Czym różni się sampling rate od bit depth?*
- *Co pokazuje spectrogram, a co waveform?*
- *Dlaczego mel-spectrogram jest popularny jako wejście do modeli?*
- *Po co resampling w preprocessing?*

---

## 4. ASR 2 — modele rozpoznawania mowy i metryki

### 4.1. Definicja ASR (w sensie modelowym)
Rozpoznawanie treści mowy z nagrania audio.  
Informacje o mówcy/stylu są wtórne — kluczowy jest **ciąg słów**.

**Cel decyzyjny:** znaleźć najlepszą hipotezę słów `w` na podstawie obserwacji akustycznych `O`.

---

### 4.2. Bayesian view (to jest klasyk egzaminowy)
Szukamy:
\[
\hat{w} = \arg\max_w P(w \mid O)
\]
Z Bayesa:
\[
P(w \mid O) \propto P(O \mid w)\,P(w)
\]

- **Acoustic model**: \(P(O \mid w)\) — jak dobrze audio pasuje do danej sekwencji słów.
- **Language model**: \(P(w)\) — jak prawdopodobna jest sekwencja słów w języku.

---

### 4.3. Acoustic modelling
Cel: estymacja \(P(O \mid w)\).  
**Słowo** często modeluje się jako sekwencję jednostek fonetycznych:
- **phoneme**: najmniejsza jednostka fonologiczna,
- **triphone**: fonem w kontekście (uwzględnia sąsiadów).

Historycznie:
- **Gaussian Mixture Models (GMM)**,
- **HMM (Hidden Markov Models)** — „klasyk”.

Współcześnie częściej:
- **sieci neuronowe** (modele hybrydowe lub end-to-end).

---

### 4.4. Language modelling
Cel: kontekst i prawdopodobieństwo sekwencji słów \(P(w)\).  
Bez LM rozpoznawanie przypomina „zgadywanie nieznanego języka ze słuchu”.

**Typy:**
- statystyczne: **n-grams**,
- neuronowe: **RNN-LM, LSTM-LM, CNN-LM**.

---

### 4.5. Klasyczne vs nowoczesne podejścia (LVCSR i E2E)
**Klasyczne (LVCSR):**
- HMM-GMM,
- hybrid,
- WFST.

**Warstwy w klasycznym ASR:**
1. akustyczna (features → zjawiska akustyczne),
2. fonetyczna (akustyka → fonemy),
3. leksykon / G2P (fonemy → słowa),
4. warstwa słów.

**End-to-end:**
- **CTC**,
- **Neural Transducer**,
- **attention models**,
- **Transformery audio** (np. wav2vec, wavLM…): audio → graphemes.

---

### 4.6. Input i output modelu
W zależności od zadania/modelu:
- **input**: waveform / spectrogram (lub inne cechy),
- **output**: tekst (ASR), waveform/spectrogram (TTS/generacja).

---

### 4.7. CTC — Connectionist Temporal Classification (intuicja)
CTC rozwiązuje problem **alignment**: jak dopasować dłuższą sekwencję ramek audio do krótszej sekwencji znaków/słów.  
Wprowadza m.in. symbol **blank** i sumuje prawdopodobieństwa po wszystkich dopuszczalnych dopasowaniach.

**Kluczowe:** CTC jest użyteczne, gdy nie masz jawnego dopasowania „co w którym momencie” w treningu.

---

### 4.8. Seq2seq (ASR i TTS)
**Seq2seq** (często z attention) mapuje sekwencje na sekwencje:
- w ASR: audio → tekst,
- w TTS: tekst → audio.

---

### 4.9. Metryki: WER (must-have)
**WER (Word Error Rate)** opiera się o dystans Levenshteina (minimalna liczba edycji).  
Operacje:
- **S** (substitution) — zamiana słowa,
- **I** (insertion) — wstawienie,
- **D** (deletion) — usunięcie.

Wzór:
\[
WER = \frac{S + I + D}{N}
\]
gdzie **N** = liczba słów w tekście referencyjnym.

**Interpretacja:** im mniejszy WER, tym lepiej.

---

### 4.10. Typowe pytania egzaminacyjne (ASR 2)
- *Wyprowadź i zinterpretuj \(\arg\max_w P(O\mid w)P(w)\). Co jest czym?*
- *Po co language model w ASR?*
- *Phoneme vs triphone — różnica i sens kontekstu.*
- *CTC: na jaki problem odpowiada i po co „blank”?*
- *WER: co mierzy, jakie ma składowe i jak go interpretować?*
- *Classic pipeline (HMM/WFST) vs end-to-end — porównanie warstw i plusów/minusów.*

---

## 5. Multimodal LLMs

### 5.1. O co chodzi w multimodalności?
Ewolucja od czystej generacji tekstu → do modeli, które rozumieją i generują na bazie wielu modalności:
- tekst,
- obraz,
- (dalej: audio, wideo).

---

### 5.2. Vision Transformer (ViT) — intuicja
**Kluczowa idea:** obraz dzieli się na **patche** (kawałki), a potem traktuje jak sekwencję tokenów (analogicznie do NLP).  
Kroki:
1. obraz → patching,
2. patch → flatten,
3. **linear projection** → embeddings,
4. encoder transformer → reprezentacja,
5. wyjście → predykcja.

To jest „most” do łączenia z LLM (łatwiej spiąć sekwencję tokenów).

---

### 5.3. Multimodal embedding models (CLIP)
Model uczy wspólną przestrzeń embeddingów dla:
- tekstu (text encoder),
- obrazu (image encoder, często ViT).

**Zastosowania CLIP / embeddingów multimodalnych:**
- **zero-shot classification**,
- klasteryzacja,
- wyszukiwanie (text→image, image→text),
- wsparcie generacji (np. jako warunkowanie).

---

### 5.4. BLIP-2: Bridging the Modality Gap
High-level architektura:
- **(zamrożony) Vision Transformer**,
- **(trenowalny) Q-Former** (Querying Transformer),
- **(zamrożony) Large Language Model**.

**Q-Former — po co?**
- ma „nauczyć się” wydobywać z obrazu informację w formie, którą LLM potrafi wykorzystać,
- typowe zadania treningowe:  
  - Image-Text Contrastive Learning,  
  - Image-Text Matching,  
  - Image-grounded Text Generation.

---

### 5.5. Preprocessing wejść multimodalnych (praktyka)
W praktyce (np. HuggingFace):
- używa się `AutoProcessor` do przygotowania wejść,
- obraz kończy jako tensory `pixel_values` o stałym rozmiarze (np. `torch.Size([1, 3, 224, 224])`),
- model dostaje odpowiednie tensory dla obrazu i tekstu.

**Ważne na egzamin:** rozumieć, że „preprocessing” jest elementem modelu/pipeline’u (resize/normalizacja/tokenizacja).

---

### 5.6. Typowe pytania egzaminacyjne (Multimodal)
- *Jak ViT zamienia obraz na sekwencję?*
- *Co to jest wspólna przestrzeń embeddingów (CLIP) i do czego służy?*
- *Dlaczego w BLIP-2 część komponentów jest zamrożona (pre-trained), a Q-Former trenowalny?*
- *Co robi Q-Former? (rola query tokens i projekcji do LLM).*

---

## Źródła (slajdy)
- Computer Vision: Fundamentals — `ZUM_CV_01.pdf`  
- Computer Vision: Detection, Segmentation, and Generative Models (Stable Diffusion) — `ZUM_CV_02.pdf`  
- Automatic Speech Recognition — `ZUM_ASR_01.pdf`  
- Automatic Speech Recognition 2 — `ZUM_ASR_02.pdf`  
- Multimodal LLMs — `ZUM_Multimodal.pdf`
