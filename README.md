Voice-Based Gender and Age Recognition Using Deep Learning

A deep learning system leveraging Long Short-Term Memory (LSTM) neural networks to predict gender and age group from voice recordings. This project processes audio features in real-time using PyAudio, offering robust gender classification and moderate age group prediction.

Table of Contents





Features



Dataset



Audio Preprocessing



Feature Extraction



Model Architecture





Gender Classification



Age Classification



Model Evaluation



Real-Time Deployment



Author



Note



References



Image References

Features





Gender Classification: Identifies speaker as male or female.



Age Group Prediction: Classifies speakers into six age groups (teens to sixties).



Real-Time Processing: Utilizes PyAudio for low-latency voice classification.



Performance Tracking: Visualizes accuracy and loss metrics for model evaluation.

Dataset

The project uses the Mozilla Common Voice Dataset (English subset).





Gender Data:





Initial: 230,000 samples.



Filtered: 97,000 balanced samples (adults aged > 20, male/female).



Visualization: Initial gender dataset distribution (initial_gender_dataset.png).



Age Data:





Initial: 250,000 samples.



Filtered: 71,000 samples (speakers < 70 years).



Age Groups: Teens, twenties, thirties, forties, fifties, sixties.



Visualization: Initial age dataset distribution (initial_age_dataset.png).

Preprocessing:





Gender dataset filtered to include only adult voices (age > 20).



Age dataset limited to speakers under 70 years.



Balanced sampling ensured fair representation across classes.

Audio Preprocessing

Audio samples are preprocessed to ensure consistency and quality:





Sample Rate: 44.1 kHz.



Mono Conversion: Converted to single-channel audio.



Silence Removal:





Global threshold: Remove segments ≤ 18 dB (audio_after_split_threshold.png).



Edge trimming: Remove start/end segments ≤ 10 dB (audio_after_trim_threshold.png).



Noise Filtering: Applied to reduce background noise.



Component Preservation: Retained harmonic (orange) and percussive (green) components for richer feature learning.



Visualization: Initial loaded audio sample (initial_loaded_audio.png).

Feature Extraction

Each audio clip is transformed into a 41-dimensional feature vector using the Librosa library:





13 Mel Frequency Cepstral Coefficients (MFCCs).



13 Delta-MFCCs (first derivatives).



13 Delta²-MFCCs (second derivatives).



1 Pitch estimate.



1 Magnitude value (smoothed with 10 ms Hann window).

Visualizations:





MFCCs and derivatives (mfcc_and_deltas_for_audio.png).



Pitch values (audio_pitches.png).



Magnitude values (audio_magnitudes.png).

Model Architecture

Gender Classification





Architecture: 2 LSTM layers (100 units each).



Dropout: 30% (first layer), 20% (second layer).



Output: Softmax layer (2 classes: male, female).



Loss Function: Categorical Crossentropy.



Optimizer: ADAM.



Training: 10 epochs.



Performance:





Validation Accuracy: 93%.



Precision: 0.94.



Visualization: Performance chart (lstm_gender_41_performance.png).

Age Classification





Architecture: 2 LSTM layers (256 units each), followed by a 256-unit dense layer (ReLU).



Dropout: 30%.



Output: Softmax layer (6 classes: teens to sixties).



Loss Function: Categorical Crossentropy.



Optimizer: ADAM.



Training: 30 epochs.



Performance:





Validation Accuracy: 49%.



Precision: 0.68.



Visualizations:





Performance chart (lstm_age_41_performance.png).



LSTM cell structure (lstm_cell.png).

Model Evaluation





Training Setup:





80-20 train-validation split.



Normalized input features (zero mean, unit variance).



Mini-batch size: 128.



Performance:





Gender model: High accuracy (93%) due to distinct vocal patterns.



Age model: Moderate accuracy (49%) due to overlapping vocal traits across age groups.

Real-Time Deployment

The system supports real-time voice classification:





Pipeline: Voice capture via PyAudio, followed by preprocessing and classification.



Latency: Minimal, enabling seamless gender and age predictions.



Applications: Suitable for personalized interfaces, accessibility tools, and demographic analysis.

Author

Pradip Giri
Master’s Student, Algoma University
Connect on LinkedIn

Note

This project is for research and educational purposes. Accuracy may vary based on:





Dataset diversity.



Recording quality.



Environmental conditions.

References





Mozilla Common Voice Dataset: https://commonvoice.mozilla.org/



Librosa Library: https://librosa.org/

Image References





initial_gender_dataset.png: Initial gender dataset distribution.



initial_age_dataset.png: Initial age dataset distribution.



initial_loaded_audio.png: Initial loaded audio sample.



audio_after_split_threshold.png: Audio after global silence removal (≤ 18 dB).



audio_after_trim_threshold.png: Audio after edge trimming (≤ 10 dB).



mfcc_and_deltas_for_audio.png: MFCCs and their derivatives.



audio_pitches.png: Pitch values from sample audio.



audio_magnitudes.png: Magnitude values from sample audio.



lstm_gender_41_performance.png: Gender model performance chart.



lstm_age_41_performance.png: Age model performance chart.



lstm_cell.png: LSTM cell structure.
