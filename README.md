[README.md](https://github.com/user-attachments/files/23391886/README.md)
# Montreal Forced Aligner (MFA) Setup and Usage Guide

This guide explains how to set up, run, and verify **Montreal Forced Aligner (MFA)** for speech-text alignment, and how to visualize the results using **Praat**.

---

```bash
# Create a new environment and install MFA
conda create -n mfa_env -c conda-forge montreal-forced-aligner -y
conda activate mfa_env
```
---

```bash
# Verify the installation
mfa version
```
---

```bash
# Download English dictionary and acoustic models
mfa model download dictionary english_us_arpa
mfa model download acoustic english_us_arpa
```
---
```bash
# Validate your dataset before alignment
mfa validate "D:\Assignment\Assignment\corpus" english_us_arpa english_us_arpa
```
**Notes:**
- Your corpus should have this structure:
  ```
  corpus/
  ├── wav/
  │   ├── file1.wav
  │   ├── file2.wav
  └── transcripts/
      ├── file1.txt
      ├── file2.txt
  ```

---

```bash
# Perform forced alignment and clean temporary files after completion
mfa align "D:\Assignment\Assignment\corpus" english_us_arpa english_us_arpa "D:\Assignment\Assignment\output" --clean
```

**Output:**
- MFA will generate `.TextGrid` files in your output directory.
- Each TextGrid file corresponds to a `.wav` file with word and phoneme alignment.

---

Once the alignment is complete, you can visualize the results using **Praat**.

### Steps:
1. Open **Praat**.
2. Go to **Open → Read from file...**
3. Load the aligned `.TextGrid` file (e.g., `F2BJRLP1.TextGrid`).
4. Load the matching `.wav` file (e.g., `F2BJRLP1.wav`).
5. In the **Praat Objects** window:
   - Select both the **Sound** and **TextGrid** objects.
   - Click **View & Edit**.
6. The waveform and alignment tiers (Words, Phonemes) will appear.
   - You can zoom, play, and inspect the alignment boundaries.
   - Use **View → Show Analyses** for additional visual layers.

---
Each TextGrid includes:
- **Words tier:** aligned word boundaries  
- **Phonemes tier:** time-aligned phoneme segments  
- Minor timing differences (~0.05–0.1 sec) are normal due to natural speech variations.

---
The Montreal Forced Aligner combines:
- **Acoustic Models** (speech-to-phoneme mapping)  
- **Pronunciation Dictionaries** (word-to-phoneme mapping)  
- **Forced Alignment Algorithms**

Together, they produce accurate word and phoneme alignment from audio–text pairs.

---
```
Assignment/
├── corpus/
│   ├── wav/
│   │   ├── F2BJRLP1.wav
│   │   ├── F2BJRLP2.wav
│   └── transcripts/
│       ├── F2BJRLP1.txt
│       ├── F2BJRLP2.txt
├── output/
│   ├── F2BJRLP1.TextGrid
│   ├── F2BJRLP2.TextGrid
└── README.md
```

---

