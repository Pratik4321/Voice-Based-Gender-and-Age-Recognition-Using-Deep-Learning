Voice-Based Gender and Age Recognition Using Deep Learning
A deep learning-powered system that predicts gender and age group based on audio recordings. This project leverages LSTM neural networks to analyze voice features and classify speaker characteristics with real-time capability.

---

Features
• Gender classification from voice
• Age group prediction (teens to sixties)
• Real-time voice processing using PyAudio
• Visual performance tracking using accuracy and loss metrics

---

Dataset
This project uses the Mozilla Common Voice Dataset (English subset).
• Gender Data: 230,000 samples → filtered to adults (age > 20) → 97,000 balanced samples (male/female)
• Age Data: 250,000 samples → filtered to speakers below 70 → 71,000 samples divided into 6 age groups:
teens, twenties, thirties, forties, fifties, sixties

• Initial gender dataset:
![initial_gender_dataset][0]

• Initial age dataset:
![initial_age_dataset][1]
Before training, we pre-processed the dataset to ensure balance and relevance:
• ➤ For the gender dataset, we included only adult voices (age > 20)
• ➤ For the age dataset, we included samples from people aged below 70
• ➤ Final training sets:
o 97,000 samples for gender, split into male and female
o 71,000 samples for age, split into 6 groups: teens, twenties, thirties, forties, fifties, sixties

---

Audio Preprocessing
• Sample Rate: 44.1kHz
• Mono conversion
• Silence removal:
o Global silence threshold: ≤ 18dB
o Start/end trimming: ≤ 10dB
• Noise filtering
• Harmonic + percussive preservation
Silence Removal Steps:

1. Global Threshold: Remove silence where volume ≤ 18dB
   Audio after first step:
   ![audio_after_split_threshold][3]
2. Trim Edges: Cut silence from start and end where volume ≤ 10dB
   Audio after second step:
   ![audio_after_trim_threshold][4]
   We preserved both harmonic (orange) and percussive (green) components for richer feature learning.

---

Feature Extraction
Each audio clip is transformed into a 41-dimensional feature vector using librosa, consisting of:
• 13 MFCCs
• 13 Delta-MFCCs
• 13 Delta²-MFCCs
• 1 Pitch Estimate
• 1 Magnitude Value
Pitch and magnitude values are smoothed with a Hann window (10ms frame).
MFCCs and their derivatives:
![mfcc_and_deltas][5]
Pitch values were smoothed with a Hann function (10ms window) before extracting the maximum.
Pitch values from sample:
![audio_pitches][6]
Magnitude values from sample:
![audio_magnitudes][7]

---

Model Architecture
1 Gender Classification
• Architecture: 2 LSTM layers (100 units)
• Dropout: 30% and 20%
• Output: Softmax (2 classes)
• Loss: Categorical Crossentropy
• Optimizer: ADAM
• Epochs: 10
• Validation Accuracy: 93%
• Precision: 0.94

---

2 Age Classification
• Architecture: 2 LSTM layers (256 units) → Fully Connected (ReLU)
• Dropout: 30%
• Output: Softmax (6 age classes)
• Loss: Categorical Crossentropy
• Optimizer: ADAM
• Epochs: 30
• Validation Accuracy: 49%
• Precision: 0.68
Age model performance chart:  
![lstm_age_41_performance][9]

---

Model Evaluation
Both models were trained with an 80-20 train-validation split and normalized input features (zero mean, unit variance). Mini-batch training was performed using a batch size of 128.
******************\_\_\_\_****************** Inference & Real-time Deployment
The final system is capable of real-time voice classification using PyAudio. After voice is captured, preprocessing and classification run seamlessly to return age and gender predictions with minimal latency.

---

Author
Pradip Giri
Master’s Student, Algoma University
Connect on LinkedIn

---

Note
This project is intended for research and educational purposes. Accuracy may vary based on dataset diversity, recording quality, and environmental conditions.

[0]: images/initial_gender_dataset.png
[1]: images/initial_age_dataset.png
[2]: images/initial_loaded_audio.png
[3]: images/audio_after_split_threshold.png
[4]: images/audio_after_trim_threshold.png
[5]: images/mfcc_and_deltas_for_audio.png
[6]: images/audio_pitches.png
[7]: images/audio_magnitudes.png
[8]: images/lstm_gender_41_performance.png
[9]: images/lstm_age_41_performance.png
[10]: images/lstm_cell.png
