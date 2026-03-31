# NEmoSen: Nepali Emotion & Sentiment Corpus

**A manually annotated multi-label emotion and sentiment dataset collected from r/Nepal (2025–2026)**

---

## Overview

NEmoSen is a multi-label emotion and sentiment corpus constructed from the Nepali Reddit community (`r/Nepal`), covering posts and comments collected between **January 2025 and February 2026**. It was introduced as part of the research paper:

> **MLESA-Net: Attention-Enhanced Multi-Label Emotion and Sentiment Analysis on Nepali Reddit Corpus**
> Nabin Kumar Rouniyar, Bibek Sah, Nayan Kumar Subhashis Behera
> School of Computer Science, KIIT Deemed to be University, Bhubaneswar, Odisha, 751024, India

NEmoSen provides a **temporally recent** complement to the existing NepEMO benchmark, capturing contemporary discourse in code-mixed Nepali text (English, Romanised Nepali, and Devanagari script).

---

## Dataset Details

| Property | Value |
|---|---|
| Total Samples | 1,059 |
| Collection Period | January 2025 – February 2026 |
| Source | r/Nepal (Reddit JSON API) |
| Language | Code-mixed (English, Romanised Nepali, Devanagari) |
| Annotation Type | Multi-label (Emotions) + Multi-class (Sentiment) |
| Avg. Words per Post | 80.8 |
| Median Words per Post | 47 |
| Avg. Emotion Labels per Sample | 1.62 |
| Missing Values | None |

---

## Schema

The dataset contains **7 columns** (`Shape: 1059 rows × 7 columns`):

| Column | Type | Description |
|---|---|---|
| `text` | `object` | Raw Reddit post/comment text (code-mixed) |
| `joy` | `int64` | Binary emotion label — Joy present (1) or absent (0) |
| `anger` | `int64` | Binary emotion label — Anger present (1) or absent (0) |
| `fear` | `int64` | Binary emotion label — Fear present (1) or absent (0) |
| `sadness` | `int64` | Binary emotion label — Sadness present (1) or absent (0) |
| `depression` | `int64` | Binary emotion label — Depression present (1) or absent (0) |
| `sentiment` | `int64` | Multi-class sentiment: `0` = Neutral, `1` = Positive, `2` = Negative |

> Multiple emotion labels can be simultaneously active for a single sample (multi-label setting). No missing values are present in any column.

---

## Label Distributions

### Emotion Labels (Binary: 0 = Absent, 1 = Present)

| Emotion | Present | Percentage |
|---|---|---|
| Joy | 399 | 37.7% |
| Anger | 474 | 44.8% |
| Fear | 327 | 30.9% |
| Sadness | 470 | 44.4% |
| Depression | 49 | 4.6% |

### Sentiment Labels

| Sentiment | Count | Percentage |
|---|---|---|
| Negative | 593 | 56.0% |
| Positive | 331 | 31.3% |
| Neutral | 135 | 12.7% |

---

## Data Collection

Posts and comments were retrieved via the **public Reddit JSON API** (no authentication required; no usernames or personal identifiers are retained). Queries were organized into five emotion-aligned keyword groups combining English and Romanised Nepali terms:

| Emotion | English Keywords | Romanised Nepali Keywords |
|---|---|---|
| Sadness | sad, depressed, heartbroken, alone, breakup | dukha, dukhi, roye, eklo |
| Anger | angry, frustrated, hate | ris, risa, jhyau, hairan, wakka |
| Fear | scared, anxiety | dar, tension, chinta, darr lagyo |
| Joy | happy, excited, proud, amazing | khusi, ramailo, maja, jeetyo |
| Surprise | shocked, unexpected, unbelievable | achamma, wow |

Up to 400 posts were retrieved per group (`restrict_sr=1`, `sort=new`). Both post bodies (title + selftext) and top-level comments were collected, with each comment treated as an independent sample. A 1-second delay between comment requests and a 2-second delay between pagination calls were applied per Reddit API rate-limit guidelines. Duplicates were removed via exact-string matching, and samples with fewer than 8 words post-cleaning were discarded.

---

## Annotation

The 1,059-sample corpus was divided into two non-overlapping partitions, with each author independently annotating their respective partition following the **NepEMO annotation schema**:

- **Five binary emotion labels**: Joy, Anger, Fear, Sadness, Depression
- **Three-class sentiment label**: Neutral (0), Positive (1), Negative (2)
- Multiple emotion labels are permitted per sample

Both authors jointly reviewed and resolved low-confidence samples through discussion. Annotation was performed by **Nabin Kumar Rouniyar** and **Bibek Sah**, under the supervision of **Dr. Nayan Kumar Subhashis Behera**.

---

## Train / Validation / Test Split

A stratified **70 / 15 / 15** split (`random_state=42`) was used in the associated research:

| Split | Samples | Percentage |
|---|---|---|
| Train | 741 | 70% |
| Validation | 159 | 15% |
| Test | 159 | 15% |

---

## Citation

If you use NEmoSen in your research, please cite:

```bibtex
@misc{nemosen2025,
  author    = {Rouniyar, Nabin Kumar and Sah, Bibek and Behera, Nayan Kumar Subhashis},
  title     = {{NEmoSen}: Nepali Emotion \& Sentiment Corpus --- a manually annotated
               multi-label Reddit dataset from {r/Nepal} (2025--2026)},
  year      = {2025},
  url       = {https://github.com/Nabin68/NEmoSen-Nepali-Emotion-Sentiment-Corpus-}
}
```

---

## ⚠️ Dataset Access

> **The dataset is available on request.**
>
> To obtain access to NEmoSen, please send a request to:
>
> 📧 **nabingupta68@gmail.com**
>
> Please include your **name**, **affiliation**, and **intended use** of the dataset in your request.
> The dataset is shared strictly for **academic and non-commercial research purposes**.

---

## License & Ethics

- Data were collected via the **public Reddit JSON API** without authentication.
- **No usernames, profile information, or personal identifiers** are retained in the dataset.
- This dataset is intended solely for **academic research** in natural language processing and affective computing.

---

## Acknowledgements

The authors thank the Nepali Reddit community (`r/Nepal`) and acknowledge the NepEMO dataset released by Sitoula et al. (2025), which informed the annotation schema used in this work. This research was conducted at **KIIT Deemed to be University, Bhubaneswar, India**, under the supervision of Dr. Nayan Kumar Subhashis Behera.
