# ZUM — Notatki cz. 2 (od nowa) — **Definicje**  
*(Computer Vision + ASR + Multimodal LLMs)*

> Ten dokument to „słownik + ściąga” pod egzamin: krótkie, precyzyjne definicje i różnice pojęć.  
> Oparte o slajdy z zajęć (CV_01, CV_02, ASR_01, ASR_02, Multimodal).  

---

## Spis treści
1. [Computer Vision — fundamenty](#computer-vision--fundamenty)  
2. [Detekcja i segmentacja](#detekcja-i-segmentacja)  
3. [Modele generatywne w CV](#modele-generatywne-w-cv)  
4. [ASR — Automatic Speech Recognition](#asr--automatic-speech-recognition)  
5. [Multimodal LLMs](#multimodal-llms)  
6. [Mini-ściąga: co z czym mylić](#mini-ściąga-co-z-czym-mylić)

---

## Computer Vision — fundamenty

### **Computer Vision (CV)**
**Definicja:** dziedzina, której celem jest **„rozumienie danych wizualnych”** (obrazów/wideo) — przejście **od pikseli do semantyki** (znaczenia).  
**Rdzeń zadań:** klasyfikacja obrazu, detekcja obiektów, segmentacja.  
**Kluczowe wyzwanie:** **generalizacja** na „real-world variability” (inne światło, tło, kamera, perspektywa).  

### **Obraz (image)**
**Definicja:** obraz cyfrowy to **macierz (lub tensor) wartości pikseli**.  
- **Piksel:** najmniejsza jednostka obrazu (wartość intensywności/koloru).  
- **Kanał (channel):** osobna warstwa informacji (np. R, G, B).  

### **Przestrzeń barw (color space)**
**Definicja:** sposób reprezentacji koloru liczbowo.  
- **RGB:** 3 kanały (Red, Green, Blue).  
- **HSV:** Hue (odcień), Saturation (nasycenie), Value (jasność).  
- **Grayscale:** 1 kanał (jasność).  
**Uwaga praktyczna:** kolejność kanałów bywa różna w bibliotekach (np. RGB vs BGR).  

### **Normalizacja / skalowanie**
**Definicja:** przekształcenie wartości pikseli do zakresu wygodnego dla modelu (np. 0–1 lub standaryzacja).  
**Po co:** stabilniejsze uczenie, spójna skala wejścia.

### **Preprocessing (wstępne przetwarzanie)**
**Definicja:** deterministyczne przygotowanie danych do modelu.  
Typowe operacje:  
- **resize** (zmiana rozmiaru), **crop** (wycięcie fragmentu), **normalize** (normalizacja).  

### **Data augmentation (augmentacja danych)**
**Definicja:** sztuczne zwiększanie różnorodności danych treningowych przez transformacje, które **nie zmieniają klasy/znaczenia** (w granicach rozsądku).  
Przykłady: rotacje, flip, „color jitter”, dodanie szumu.  
**Po co:** lepsza generalizacja, mniejsze overfitting.

### **Klasyczne CV (classical computer vision)**
**Definicja:** podejście oparte o **ręcznie projektowane cechy** i filtry.  
- **Edge detection:** np. Sobel, Canny — wykrywanie krawędzi.  
- **Feature extraction:** np. SIFT, HOG — opisy obrazu jako wektory cech.  
- **Segmentation (klasyczna):** np. thresholding, watershed.  
**Ograniczenie:** cechy są często „domain-specific” (słabo przenoszą się na nowe dane).

### **Deep Learning w CV**
**Definicja:** modele uczą się **hierarchicznych cech automatycznie** (od prostych krawędzi → do złożonych obiektów).  
**Dlaczego działa:** duże zbiory + GPU + architektury (np. CNN).

### **CNN (Convolutional Neural Network)**
**Definicja:** sieć neuronowa zaprojektowana do pracy na danych „siatkowych” (np. obrazach), wykorzystująca **splot (convolution)**.  
Typowy pipeline:  
1. **Convolutional layer** — ekstrakcja cech (filtry/kernele)  
2. **Pooling** — downsampling (zmniejszanie rozdzielczości cech)  
3. **Activation (np. ReLU)** — nieliniowość  
4. **Fully connected** — klasyfikacja (na końcu)  

### **Popularne architektury CNN**
**Definicje skrótowe (co je wyróżnia):**  
- **LeNet:** wczesne CNN (np. cyfry).  
- **AlexNet:** przełom w ImageNet (skalowanie + głębsza sieć).  
- **VGG:** „głębiej i prościej” (powtarzalne bloki).  
- **ResNet:** **skip connections** (połączenia omijające) → bardzo głębokie sieci bez degradacji uczenia.

### **Transfer learning**
**Definicja:** ponowne użycie **pretrenowanego** modelu (np. na ImageNet) do nowego zadania.  
- **Fine-tuning:** delikatne douczenie (części lub całości).  
- **Freeze layers:** zamrożenie „dolnych” warstw (cechy ogólne) i uczenie głównie klasyfikatora.  
**Po co:** szybciej i mniej danych potrzeba.

---

## Detekcja i segmentacja

### **Klasyfikacja (image classification)**
**Definicja:** model zwraca **jedną etykietę dla całego obrazu** (np. „kot”).  
**Wyjście:** klasa / rozkład prawdopodobieństw klas.

### **Detekcja obiektów (object detection)**
**Definicja:** model odpowiada na pytanie **„co” i „gdzie”** — wykrywa wiele obiektów i lokalizuje je.  
**Wyjście:** lista obiektów, zwykle w formie **bounding boxes + class labels**.

### **Bounding box (ramka)**
**Definicja:** prostokąt opisujący położenie obiektu w obrazie (np. x, y, width, height).

### **Segmentacja (segmentation)**
**Definicja:** **klasyfikacja na poziomie piksela** — każdy piksel dostaje etykietę klasy.  

### **Semantic segmentation**
**Definicja:** każdy piksel ma klasę, ale **nie rozróżniasz instancji** (np. „człowiek” jako jedna masa).

### **Instance segmentation**
**Definicja:** segmentacja, która **oddziela instancje tego samego obiektu** (np. 3 osoby → 3 maski).

### **Ewolucja metod detekcji**
**Definicje „rodzin” podejść:**  
- **Sliding windows:** przesuwane okna + klasyfikator (stare, wolne).  
- **Region proposals:** najpierw generujesz kandydatów regionów, potem je klasyfikujesz.  
- **End-to-End models:** jeden model uczy się wykrywać bez osobnych etapów.

### **Rodziny modeli detekcji**
- **R-CNN / Fast R-CNN / Faster R-CNN (region-based):** detekcja oparta o regiony (zwykle dokładna, bywa wolniejsza).  
- **YOLO (You Only Look Once):** „single-shot” detektor, **real-time**.  
- **SSD (Single Shot Multibox Detector):** kompromis szybkość vs dokładność.  
**Trade-off:** precyzja vs czas inferencji.

---

## Modele generatywne w CV

### **Model generatywny (generative model)**
**Definicja:** model, który uczy się **rozkładu danych** (jak wyglądają obrazy z danej domeny), by **tworzyć nowe próbki**.  
Zastosowania: generowanie obrazów, augmentacja, super-resolution.

### **GAN (Generative Adversarial Network)**
**Definicja:** uczenie przez „grę” dwóch sieci:  
- **Generator:** tworzy fake próbki.  
- **Discriminator:** odróżnia fake od real.  
**Typowe problemy:** **mode collapse**, niestabilna zbieżność.

### **VAE (Variational Autoencoder)**
**Definicja:** autoenkoder probabilistyczny, który mapuje dane do **przestrzeni latentnej** i potrafi z niej generować; kładzie nacisk na „gładką” latent space (łatwiejsze próbkowanie).

### **Diffusion model (model dyfuzyjny)**
**Definicja:** generowanie przez **odszumianie**:  
- **Forward process:** obraz → stopniowo dodajesz szum aż do „noise”.  
- **Reverse process:** noise → uczysz się odwracać proces, czyli **denoising** → obraz.  
**Plus:** stabilniejsze, wysokiej jakości generowanie.

### **Stable Diffusion (intuicyjny pipeline prompt→image)**
**Definicja procesu:**  
**Text → embedding → latent noise → denoising → image**.  
- **Seed:** kontroluje losowość (ten sam seed + prompt → podobne wyniki).  
- **Prompt strength:** jak mocno trzymać się promptu.

### **Fine-tuning / kontrola generowania**
- **DreamBooth:** personalizacja modelu niewielką liczbą obrazów (uczenie „konkretnego obiektu/stylu”).  
- **LoRA (Low-Rank Adaptation):** lekka adaptacja (mało parametrów, „tani” tuning).  
- **ControlNet:** dodatkowe warunki wejściowe (np. krawędzie, głębia, poza).

---

## ASR — Automatic Speech Recognition

### **ASR (Automatic Speech Recognition)**
**Definicja:** rozpoznawanie **treści mowy** na podstawie nagrania audio, z pominięciem informacji o mówcy i sposobie mówienia (liczy się sekwencja słów).  

### **Waveform (przebieg czasowy)**
**Definicja:** sygnał audio jako funkcja amplitudy w czasie.

### **Sampling rate (częstotliwość próbkowania)**
**Definicja:** ile próbek sygnału zapisujesz na sekundę (Hz).  
**Intuicja:** wyższa → lepsze odwzorowanie wysokich częstotliwości, większe dane.

### **Bit depth (głębia bitowa)**
**Definicja:** ile bitów opisuje pojedynczą próbkę amplitudy.  
**Intuicja:** większa → większa precyzja amplitudy, mniejsze szumy kwantyzacji.

### **Frequency (częstotliwość)**
**Definicja:** składowa „jak szybko drga” sygnał; w mowie kluczowa dla barwy/głosek.

### **Spectrogram (spektrogram)**
**Definicja:** reprezentacja czasu–częstotliwości: pokazuje, jakie częstotliwości są obecne w czasie (często wejście do modeli).

### **Mel spectrogram**
**Definicja:** spektrogram przekształcony do skali **Mel** (bardziej „percepcyjnej” dla ludzkiego słuchu).

### **Model wejścia/wyjścia w audio**
**Wejście (input):** tekst / waveform / spektrogram.  
**Wyjście (output):** tekst / waveform / spektrogram (zależnie od zadania).  

### **Bayes w ASR (dekodowanie)**
**Cel:** znaleźć najlepszą hipotezę tekstu.  
W ujęciu bayesowskim:  
- **Acoustic model:** P(O|w) — prawdopodobieństwo obserwacji audio O dla sekwencji słów w.  
- **Language model:** P(w) — prawdopodobieństwo sekwencji słów (sensowność językowa).

### **Acoustic modeling**
**Definicja:** modelowanie P(O|w) — na ile obserwacje pasują do słów.  
**Słowo jako sekwencja jednostek fonetycznych:**  
- **Phoneme (fonem):** abstrakcyjna jednostka językowa, najmniejszy „element rozróżniający” w danym języku.  
- **Triphone:** fonem w kontekście sąsiadów (uwzględnia wpływ otoczenia).  
Historycznie: **GMM** + **HMM**; współcześnie często **sieci neuronowe**.

### **Language modeling**
**Definicja:** ustalanie kontekstu słownego wypowiedzi; model P(w).  
- **Statystyczne:** **n-grams**.  
- **Neural:** np. RNN-LM, LSTM-LM, CNN-LM.

### **Klasyczne vs nowoczesne podejścia**
**Classic LVCSR:** HMM-GMM, hybrydy, WFST.  
**Warstwy (pipeline):**  
1) akustyczna (cechy → zjawiska akustyczne)  
2) fonetyczna (akustyka → fonemy)  
3) leksykon + G2P (fonemy → słowa)  
4) warstwa słów  
**End-to-end:** CTC, Neural Transducer, modele attention; transformery audio (np. wav2vec, wavLM), często **audio → graphemes**.

### **CTC (Connectionist Temporal Classification)**
**Definicja:** funkcja celu dla modeli sekwencyjnych, gdy nie masz jawnego wyrównania (alignment) między ramkami audio a znakami; pozwala uczyć mapowania audio→tekst bez ręcznego alignowania.

### **WER (Word Error Rate)**
**Definicja:** metryka jakości ASR oparta o **odległość Levenshteina** (minimalna liczba edycji).  
Operacje: **Substitutions (S)**, **Insertions (I)**, **Deletions (D)**.  
Wzór:  
WER = (S + I + D) / N  
gdzie N = liczba słów w transkrypcji referencyjnej.

---

## Multimodal LLMs

### **Multimodal LLM**
**Definicja:** model (zwykle oparty o transformery), który przetwarza **więcej niż jedną modalność** (np. tekst + obraz, czasem też audio/wideo) i potrafi generować/wnioskować na ich podstawie.

### **Vision Transformer (ViT)**
**Definicja:** transformer zastosowany do obrazu: obraz dzielisz na **patche**, mapujesz na wektory (embeddingi) i przetwarzasz mechanizmem attention (analogicznie do tokenów w NLP).

### **Multimodal embedding model**
**Definicja:** model uczący wspólną przestrzeń wektorową (embedding space), gdzie **teksty i obrazy** mogą być porównywane (np. podobieństwo kosinusowe).

### **CLIP**
**Definicja (intuicyjna):** model łączący tekst i obraz w jednej przestrzeni embeddingów.  
Zastosowania: **zero-shot classification**, **clustering**, **search**, **generation**.

### **Vision–Language Models (VLM)**
**Definicja:** modele łączące percepcję obrazu z generacją/rozumieniem języka (np. odpowiadanie na pytania o obraz, captioning).

### **BLIP-2**
**Definicja (z idei slajdów):** architektura „bridging the modality gap” — łączy enkoder wizji z LLM przez komponent pośredniczący.

### **Q-Former**
**Definicja:** moduł pośredni (query-based), który „wyciąga” z obrazu reprezentacje najbardziej przydatne dla LLM i mapuje je do formatu zgodnego z modelem językowym.

### **Trzy cele uczenia w BLIP-2 (w skrócie)**
- **Image-Text Contrastive Learning:** zbliżanie par (obraz, opis) w embeddingach, odsuwanie niepasujących.  
- **Image-Text Matching:** klasyfikacja „czy tekst pasuje do obrazu”.  
- **Image-grounded Text Generation:** generacja tekstu uwarunkowana obrazem (np. opis, odpowiedź).

### **Preprocessing multimodal inputs**
**Definicja:** standardowe przygotowanie wejść w różnych modalnościach:  
- **Image preprocessing:** resize/normalize, patchowanie (ViT).  
- **Text preprocessing:** tokenizacja, embedding tokenów.

---

## Mini-ściąga: co z czym mylić

### Klasyfikacja vs detekcja vs segmentacja
- **Klasyfikacja:** *co jest na obrazie?* (1 etykieta)  
- **Detekcja:** *co i gdzie?* (ramki + klasy)  
- **Segmentacja:** *gdzie dokładnie?* (maski pikselowe)  
- **Instance segmentation:** *gdzie dokładnie i ile sztuk?* (osobne maski)

### Klasyczne CV vs Deep Learning
- **Klasyczne CV:** ręczne cechy (SIFT/HOG), filtry (Canny)  
- **DL:** cechy uczone automatycznie (CNN/ViT)

### ASR: Acoustic model vs Language model
- **Acoustic:** dopasowanie dźwięku do słów P(O|w)  
- **Language:** sensowność sekwencji słów P(w)

### Spectrogram vs Mel-spectrogram
- **Spectrogram:** fizyczna reprezentacja czasu–częstotliwości  
- **Mel:** „skala słuchowa” → często wygodna dla mowy

### Multimodal embedding vs Multimodal LLM
- **Embedding model (np. CLIP):** wspólna przestrzeń podobieństwa obraz–tekst  
- **Multimodal LLM:** rozumowanie + generacja w oparciu o wiele modalności (często korzysta z embeddingów/enkoderów)

---

## Źródła (slajdy)
- ZUM_CV_01.pdf  
- ZUM_CV_02.pdf  
- ZUM_ASR_01.pdf  
- ZUM_ASR_02.pdf  
- ZUM_Multimodal.pdf
