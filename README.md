# Libyan Telecom Sentiment Analysis Dataset

**Original, unprocessed Libyan Arabic social-media comments for sentiment analysis research**

**Researcher / repository maintainer:** Almahdi Elzalouk  
**Related research:** *A Comparative Study on Overfitting Control in Libyan Sentiment Analysis Models*  
**Research DOI:** https://doi.org/10.36602/ijeit.v15i1.755

## Overview

This repository provides three original sentiment-labeled datasets of user comments concerning major telecommunications providers in Libya: **Libyana**, **Almadar Aljadid**, and **Libya Telecom and Technology (LTT)**. The datasets contain **8,560 records** in total and can support research into Libyan Arabic sentiment analysis, dialectal natural language processing, class imbalance, and model generalization.

The repository is maintained in connection with Almahdi Elzalouk's research on **overfitting control in Libyan sentiment analysis models**. That work investigates classification performance and generalization across individual telecom datasets using machine-learning approaches. The repository makes the input datasets easier to discover and interpret; it does **not** claim that Elzalouk originally collected or annotated the comments.

## Dataset files and statistics

| Dataset | Original file | Records | Label `0` | Label `1` |
| --- | --- | ---: | ---: | ---: |
| Libyana | `Libyana company Dataset.xlsx` | 6,566 | 5,015 | 1,551 |
| Almadar Aljadid | `Almadar company Dataset.xlsx` | 1,784 | 1,240 | 544 |
| Libya Telecom and Technology | `Libya Telecom and Technology company Dataset.xlsx` | 210 | 151 | 59 |
| **Total** | | **8,560** | **6,406** | **2,154** |

These counts were checked directly against the supplied Excel files. The table reports the **stored numeric labels** and does not silently reinterpret or modify them.

**Important label caveat:** The original publication reports 151 positive and 59 negative LTT examples, whereas the supplied LTT spreadsheet contains 151 records labeled `0` and 59 labeled `1`. If using `1 = positive` and `0 = negative` consistently across all three files, these do not agree. Users should verify the LTT label mapping against the original source before interpreting polarity; the records and labels here have intentionally not been corrected.

## Data schema

All three workbooks contain the following columns:

| Column | Description |
| --- | --- |
| `UserScreenName` | Display name recorded for the posting account |
| `UserName` | Account handle recorded in the source |
| `Timestamp` | Recorded posting timestamp |
| `Text` | Original comment / tweet text |
| `Class` | Original numeric sentiment class (`0` or `1`) |
| `Emojis` | Emoji field where available |
| `Comments` | Recorded comment or reply count where available |
| `Likes` | Recorded like count where available |
| `Retweets` | Recorded repost/retweet count where available |
| `Image link` | Source image link where available |
| `Tweet URL` | Source post URL where available |

Blank cells should be interpreted as missing values, not automatically as zero.

## Raw data policy and preprocessing

**The provided datasets are preserved exactly as supplied.** No new cleaning, normalization, filtering, deduplication, translation, tokenization, stemming, lemmatization, re-annotation, or other preprocessing has been applied by this repository. Existing values, column names, and annotations are retained.

**Preprocessing is the responsibility of each researcher.** Users should document any transformations and keep their processed outputs separate from the original workbooks so their experiments remain reproducible.

## Loading the data

Python 3 and `pandas` with an Excel reader such as `openpyxl` can load the workbooks:

```bash
pip install pandas openpyxl
```

```python
from pathlib import Path

import pandas as pd

data_dir = Path(".")
files = {
    "libyana": "Libyana company Dataset.xlsx",
    "almadar": "Almadar company Dataset.xlsx",
    "ltt": "Libya Telecom and Technology company Dataset.xlsx",
}

datasets = {
    company: pd.read_excel(data_dir / filename)
    for company, filename in files.items()
}

for company, frame in datasets.items():
    print(company, len(frame), frame["Class"].value_counts().to_dict())
```

This example **reads** the files only; it does not change or save them.

## Research contribution

Elzalouk's associated research, *A Comparative Study on Overfitting Control in Libyan Sentiment Analysis Models*, examines how machine-learning evaluation choices and overfitting-control strategies affect classification on Libyan Arabic sentiment data. This repository provides access to the **original inputs** relevant to that line of research rather than distributing any particular cleaned or model-ready variant.

**Related publication:** https://doi.org/10.36602/ijeit.v15i1.755

## Original data source and attribution

The tweets were **originally collected and manually annotated by AbdulHamid Omar, Mansour Essgaer, and Khamiss M. S. Ahmed**, not by the maintainer of this repository. According to their 2022 study, collection used the Twitter API during January–December 2020, and three human annotators assigned sentiment categories using majority voting. Their initial collection contained 16,730 posts, from which the labeled subsets were obtained.

Please credit the original corpus creators when using the data:

> A. Omar, M. Essgaer, and K. M. S. Ahmed, “Using Machine Learning Model To Predict Libyan Telecom Company Customer Satisfaction,” *2022 International Conference on Engineering & MIS (ICEMIS)*, 2022. doi: [10.1109/ICEMIS56295.2022.9914055](https://doi.org/10.1109/ICEMIS56295.2022.9914055).

Original corpus repository: https://github.com/Mansour-Essgaer/Libya-Telecom-companies-corpus

## Citation

For research building on Elzalouk's overfitting-control study, cite the related article using its publisher-provided bibliographic metadata:

> *A Comparative Study on Overfitting Control in Libyan Sentiment Analysis Models*. https://doi.org/10.36602/ijeit.v15i1.755

When using these datasets themselves, **also cite the original data-collection paper above**. Citing the related research does not replace credit to the original dataset authors.

## Responsible use and redistribution

The files may contain public account display names, handles, timestamps, and direct post or media URLs. Researchers should consider applicable privacy expectations, platform terms, and ethical requirements before republishing, joining, or redistributing individual records.

**Redistribution permission has not yet been verified.** This README does not grant a license to reuse or redistribute third-party content. The original author's repository and any applicable platform terms should be checked before making the workbooks publicly accessible. Until that verification is complete, the README may be published independently while the datasets remain unpublished.

## Scope

This repository covers **only the three Libyan telecom datasets**. The separate Libyan poetry corpus used in other research is not included.
