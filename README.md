# MER-Emotion-Estimator

Questo repository contiene l’implementazione di un sistema di **Music Emotion Recognition (MER)** basato su deep learning, finalizzato alla **predizione dinamica di valence e arousal** a partire da segnali audio musicali.

Il modello utilizza **mel-spectrogrammi** estratti da segmenti audio di **1 secondo** e una **architettura CRNN (CNN + GRU)** addestrata sul **DEAM Dataset** con annotazioni dinamiche per secondo.

---

## 📌 Obiettivo

L’obiettivo del progetto è stimare automaticamente le dimensioni emozionali fondamentali:

- **Valence** → emozione positiva / negativa  
- **Arousal** → livello di attivazione / energia  

in modo **continuo nel tempo**, producendo una predizione emozionale per ogni secondo del brano musicale.

Il sistema è pensato come base per:

- analisi emozionale musicale
- visualizzazioni audio–reattive
- arte generativa guidata dall’emozione
- ricerca accademica in Music Emotion Recognition

---

## 🎧 Dataset

### DEAM – Database for Emotion Analysis using Music

Il progetto utilizza il **DEAM Dataset**, che include:

- 🎵 brani musicali in formato `.mp3`
- 📈 annotazioni dinamiche di valence e arousal
- 👥 valutazioni di più annotatori
- ⏱ campionamento temporale per secondo
  
### 1️⃣ Segmentazione audio

- Sample rate: **44.1 kHz**
- Segmentazione in finestre di **1 secondo**
- Ogni finestra rappresenta uno stato emozionale temporale

Per ogni segmento audio viene calcolato:

- **Mel-Spectrogram**
- 128 bande mel
- `n_fft = 2048`
- `hop_length = 512`
- conversione in scala logaritmica (dB)

### Dettagli

- **CNN**
  - Conv2D: 32 → 64 → 128
  - Batch Normalization
  - MaxPooling
  - Dropout

- **RNN**
  - GRU (128 unità)
  - modellazione temporale dell’emozione

- **Output**
  - 2 neuroni
  - attivazione lineare
  - regressione continua

---

## 🏋️ Training

- Optimizer: **Adam**
- Learning rate: `1e-3`
- Loss: **Mean Squared Error (MSE)**
- Metriche: **MAE**

### Callback

- EarlyStopping
- ModelCheckpoint
- ReduceLROnPlateau
Durante l’addestramento vengono tracciate:

- training loss vs validation loss
- training MAE vs validation MAE

utili per analizzare convergenza e overfitting.
