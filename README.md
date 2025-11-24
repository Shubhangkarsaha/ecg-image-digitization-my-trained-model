# ecg-image-digitization-my-trained-model

🫀 PhysioNet 2025 — ECG Image Digitization
Reconstructing true 12-lead ECG signals from ECG images
📌 Overview

Electrocardiograms (ECGs) have guided heart-disease diagnosis for decades. Modern ECG machines store signals as time-series data, but around the world, billions of ECGs still exist only as:

Printed thermal paper strips

Scanned copies

Photographs

Image-only digital files

These images cannot be used directly by medical-grade tools or ML models that rely on accurate time-series inputs. This competition aims to bridge that gap by converting ECG images → true 12-lead digital signals.

✔️ Unlock decades of archived ECGs
✔️ Enable more powerful ML models for cardiac diagnosis
✔️ Improve global access to high-quality cardiac insights

🖼️ Why Digitizing ECG Images Is Hard

ECG images aren’t simple pictures—they contain delicate medical signals. Several real-world issues complicate extraction:

Imaging Artifacts

Rotation, skew, reflection

Lighting variations, blur

Low-resolution scans

Camera distortions

Aspect ratio changes

Paper and Printing Issues

Faded thermal paper

Fold marks, smudges

Ink discontinuities

Partial cropping

ECG-Specific Challenges

Vendor-specific layouts

Variations in lead positions

Multiple sampling frequencies

Baseline drift & original signal noise

Because accuracy affects clinical interpretation (e.g., PR, QRS, QT intervals), even small errors matter.

📈 Competition Goal

Build a model that takes an ECG image and reconstructs the original 12-lead time-series waveform.
The output should match the ground-truth signal as closely as possible.

📊 Evaluation Metric — Modified SNR

The competition uses a modified Signal-to-Noise Ratio (SNR) to measure reconstruction quality.

Before comparing predicted vs. true signals, it corrects for:

1️⃣ Time Shift (≤ 0.2 sec)

Finds the best horizontal alignment via cross-correlation.

2️⃣ Amplitude Offset

Removes constant vertical bias.

Final Score

After alignment, SNR is computed across all 12 leads combined.
Higher SNR (dB) → better signal restoration → better leaderboard rank.

🧩 Suggested Pipeline (High-Level)

A practical digitization system often includes:

1. Preprocessing

Deskew photos

Denoise scanned images

Detect grid lines

Correct perspective distortion

2. Lead Localization

Detect each lead panel

Crop regions accurately

3. Trace Extraction

Identify ink pixels

Track the waveform using skeletonization or segmentation

Convert pixels → amplitude using grid scale

4. Signal Refinement

Remove baseline wander

Smooth residual noise

Resample to standard frequencies

Use a small neural network for fine correction

5. Metric-Aware Training

Incorporate alignment logic during validation

Optimize directly for SNR improvement

📁 Submission Format

Your submission file must be either:

submission.csv
submission.parquet


Format:

id,value
62_0_I,0.0
62_1_II,0.3
62_2_I,0.4
...
