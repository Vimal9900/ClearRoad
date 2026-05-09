# ClearRoad

**A Benchmark for Multiple Degradation Restoration in Dash-Cam Footage**

[![Frames](https://img.shields.io/badge/Frames-15M%2B-blue?style=flat-square)](#)
[![Annotated](https://img.shields.io/badge/Annotated-82K_frames-orange?style=flat-square)](#)
[![Degradations](https://img.shields.io/badge/Degradations-7_types-red?style=flat-square)](#)
[![Resolution](https://img.shields.io/badge/Resolution-1920×1080-purple?style=flat-square)](#)
[![License](https://img.shields.io/badge/License-Research_Only-green?style=flat-square)](#)

---

ClearRoad is a large-scale, real-world dataset for multi-degradation image restoration (MDIR) in driving scenarios. Unlike existing benchmarks that rely on synthetic weather composites, every frame in ClearRoad comes from actual dashcam footage — collected across 7,000 km of driving under naturally occurring haze, rain, and out-of-focus conditions. The dataset spans 15 million frames, 7 degradation categories, and 82,165 manually annotated frames with object-level labels.

This repository hosts **3,500 curated sample images** (500 per category) for quick evaluation and reproducibility checks.

---

## Dataset at a Glance

| | |
|---|---|
| Total frames | 15,203,303 |
| Annotated frames | 82,165 |
| Annotation hours | 1,000+ |
| Driving distance | ~7,000 km |
| Recording duration | ~138 hours |
| Resolution | 1920 × 1080 @ 30 fps |
| Cameras | GoPro Hero 7 · Samsung M32 · iPhone 14 Pro |
| Raw data volume | ~1.3 TB |

---

## Sample Images

The collage below shows representative frames from all seven degradation types under both day and night conditions.

![Degradation Collage](collage_degradation.jpg)

*Top row: daytime scenes — Light Haze (LH), Medium Haze (MH), Dense Haze (DH), Rain Streak (RS), Raindrop (RD), Out-of-Focus (OoF). Bottom row: corresponding night-time scenes.*

---

## Frame Distribution

| Category | Degradation Type | Total Frames | Annotated |
|---|---|---:|---:|
| Haze | Light Haze | 1,180,350 | 15,722 |
| | Medium Haze | 342,080 | 4,293 |
| | Dense Haze | 433,150 | 5,503 |
| Rain | Rain Streak | 253,000 | 3,264 |
| | Raindrop | 2,293,592 | 1,184 |
| Out-of-Focus | (all conditions) | 36,731 | 3,000 |
| Clear | Clear Weather | 10,664,400 | 49,199 |
| **Total** | | **15,203,303** | **82,165** |

> **Note:** The Out-of-Focus subset is drawn from across Haze (4,420 frames), Rain (6,711 frames), and Clear (25,600 frames) recording sessions, capturing sensor-induced blur under varied weather conditions.

---

## Train / Test Split

The dataset is partitioned into training and test sets. The training split includes both annotated and unannotated frames, supporting supervised, semi-supervised, and unsupervised model development. The test split contains only fully annotated samples to ensure reliable and reproducible evaluation.

| Subset | Train | Test | Total |
|---|---:|---:|---:|
| Light Haze | 1,178,350 | 2,000 | 1,180,350 |
| Medium Haze | 340,080 | 2,000 | 342,080 |
| Dense Haze | 431,150 | 2,000 | 433,150 |
| Rain Streak | 251,000 | 2,000 | 253,000 |
| Raindrop | 2,292,592 | 1,000 | 2,293,592 |
| Out-of-Focus | 34,731 | 2,000 | 36,731 |
| Day | 6,483,050 | 1,000 | 6,484,050 |
| Night | 4,179,350 | 1,000 | 4,180,350 |

> The Day and Night subsets are two additional cross-cutting views of the dataset that cover all degradation types; they are not counted separately in the total frame count.

---

## Object Annotation Counts

Fine-grained object-level annotations cover 82,165 frames across seven object categories.

| Condition | Vehicle | Pedestrian | Bike | Bird | Animal | Bicycle | Helicopter | Total |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Light Haze | 27,218 | 18,995 | 28,417 | 1,163 | 784 | 7,549 | 2 | 84,128 |
| Medium Haze | 1,886 | 931 | 480 | 135 | 95 | 114 | 0 | 3,641 |
| Dense Haze | 931 | 707 | 350 | 5 | 21 | 121 | 0 | 2,135 |
| Rain Streak | 10,599 | 1,307 | 4,313 | 1,359 | 197 | 111 | 0 | 17,886 |
| Raindrop | 3,001 | 356 | 1,119 | 52 | 15 | 35 | 0 | 4,578 |
| Out-of-Focus | 2,730 | 94 | 419 | 22 | 29 | 20 | 0 | 3,314 |
| Clear | 105,872 | 28,922 | 46,753 | 8,675 | 4,974 | 6,466 | 65 | 201,727 |
| **Day** | **83,768** | **39,027** | **60,092** | **6,717** | **2,884** | **13,254** | **20** | **205,762** |
| **Night** | **65,886** | **12,318** | **21,430** | **4,713** | **3,223** | **1,187** | **47** | **108,804** |

> Day and Night rows reflect cross-cutting illumination subsets; they overlap with the degradation-specific rows above and are not additive to the total.

---

## Repository Structure

The sample data is organized hierarchically by weather conditions and illumination:

```
sample_data/
├── Day/                         # 500 frames — daytime scenes (all weather types)
├── Night/                       # 500 frames — nighttime scenes (all weather types)
├── Clear/                       # Clear weather category
│   ├── Clear/                   # Clear weather samples
│   └── OoF(Out of Focus)/       # Out-of-focus frames (clear conditions)
├── Haze/                        # Haze/atmospheric degradation category
│   ├── Light Haze/              # Light atmospheric haze samples
│   ├── Medium Haze/             # Moderate atmospheric haze samples
│   ├── Dense Haze/              # Heavy atmospheric haze samples
│   └── OoF(Out of Focus)/       # Out-of-focus frames (haze conditions)
├── Rain/                        # Rain-related degradation category
│   ├── Raindrop/                # Raindrop-on-lens artifact samples
│   ├── RainStreak/              # Rain streak on lens samples
│   └── OoF(Out of Focus)/       # Out-of-focus frames (rain conditions)
└── collage_degradation.jpg      # Visual overview across all degradation types
```

**Sample Distribution:**
- **Day & Night:** 500 frames each (cross-cutting across all degradations)
- **Clear, Haze, Rain:** Hierarchical groupings with subcategories (structure prepared for sample expansion)

All images are HD JPG (1920 × 1080), captured from a dashcam mounted below the rear-view mirror.

---

## Data Collection

Footage was recorded across urban roads, highways, and countryside spanning diverse geographic regions. Weather windows were targeted using open-source forecast APIs: haze conditions account for 1,091 minutes of recording, rain for 1,421 minutes, and clear weather (including night, low-light, and flare conditions) for 5,940 minutes — totalling approximately 8,272 minutes (~138 hours) of driving across roughly 7,000 km.

Frames were filtered for quality using BRISQUE perceptual scores and the Brenner Gradient for sharpness. Degradation labels were assigned via a semi-automated pipeline — the Dark Channel Prior for haze intensity estimation, blob detection for raindrop identification, and the Brenner Gradient for out-of-focus detection — validated against a manually annotated seed set with over 75% inter-annotator agreement.

Three consumer-grade cameras were used: GoPro Hero 7 (60% of footage), Samsung M32 (30%), and iPhone 14 Pro (10%), ensuring variability in sensor characteristics such as noise cancellation, compression, and colour reproduction.

---

## Benchmarking

ClearRoad enables evaluation using no-reference image quality metrics (PIQE, NIQE, BRISQUE, FADE), since clean reference frames are unavailable in real driving footage. Benchmarking across 10 supervised and 4 unsupervised state-of-the-art restoration methods reveals substantial performance degradation under real-world conditions compared to results reported on existing synthetic benchmarks — underscoring the sim-to-real gap and the necessity of a dataset like ClearRoad.

See the paper for full results and analysis.

---

## Citation

```bibtex
@article{clearroad2026,
  title   = {ClearRoad: A Benchmark for Multiple Degradation Restoration in Dash-Cam Footage},
  author  = {},
  year    = {2026},
}
```

> Citation will be updated upon publication.

---

## License

This sample data is released for **research and non-commercial use** only.

---

## Contact

For questions about the full dataset, annotation access, or collaboration, please visit the [anonymous archive](https://anonymous.4open.science/r/ClearRoad-680E/) or contact via the submission portal.
