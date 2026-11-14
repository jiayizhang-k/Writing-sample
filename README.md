# Writing Sample: Douban Reviews of *The Blue Kite*

Code and results for my writing sample on how Chinese viewers interpret *The Blue Kite* (蓝风筝, dir. Tian Zhuangzhuang, 1993), a film banned in mainland China that follows one family through the Anti-Rightist Campaign, the Great Leap Forward, and the Cultural Revolution.

> ### 📄 All analysis code: [`blue_kite_analysis.Rmd`](blue_kite_analysis.Rmd)
> ### 🗺️ Interactive topic map (Figure 1): [open in your browser](https://jiayizhang-k.github.io/Writing-sample/results/LDAvis_seeded_en.html)
> Terms shown in English and Chinese; switch to [English only](https://jiayizhang-k.github.io/Writing-sample/results/LDAvis_seeded_en.html?lang=en) or [Chinese only](https://jiayizhang-k.github.io/Writing-sample/results/LDAvis_seeded_en.html?lang=zh).

**Research question.** How do viewers of *The Blue Kite* interpret the suffering it shows under the revolutionary order, and how do they construct competing explanations of its causes and of who bears responsibility?

## Code

**All analysis code is in [`blue_kite_analysis.Rmd`](blue_kite_analysis.Rmd)** (R Markdown). It runs the full pipeline, from cleaning the reviews to the topic models, stability checks, robustness checks, and figures.

| Section | Contents |
|---|---|
| 0–2 | Packages; loading and cleaning; tokenization and stopwords |
| 3–6 | Word counts and collocates; export of *kefu* passages for hand coding; paragraph corpus |
| 7 | t-SNE word maps |
| 8 | Unsupervised LDA: choosing k, 100 fits, most typical fit, stability |
| 9 | Seeded LDA: seed rules, 100 fits, stability, and the gender test (with its possible outcomes stated in advance) |
| 10 | Where key unseeded words land |
| 11 | Robustness: random starts, residual topics, alternative dictionaries, review-level model |
| 12 | LDAvis topic map |

## Pipeline

Computational methods are used to guide close reading, not to replace it.

1. **Preprocessing** (`quanteda`): Chinese word segmentation with character names kept as single tokens; standard and custom stopword lists; paragraphs as documents (1,989 paragraphs); words used at least 5 times in at least 3 paragraphs.
2. **Exploratory maps** (`Rtsne`): t-SNE of the 80 most frequent and the 80 most distinctive (TF-IDF) words.
3. **Unsupervised LDA**: k = 8, chosen after comparing values of k from 4 to 15; 100 fits from different random starts.
4. **Seeded LDA** (`seededlda`): a seed dictionary of 7 topics, built from the exploratory models with explicit rules for each seed word, plus 3 residual topics; 100 fits.
5. **Close reading and hand coding**: every quoted review was read in full. Two coding schemes (the folk belief *kefu* and the attribution of responsibility) are described in the paper's appendix.

## Results

Key outputs from the final run, in [`results/`](results/):

| Paper | File |
|---|---|
| Figure 1: seeded LDA topic map | [Interactive map](https://jiayizhang-k.github.io/Writing-sample/results/LDAvis_seeded_en.html) (`LDAvis_seeded_en.html`); Chinese original `LDAvis_seeded_standalone.html` |
| Figures A1–A2: t-SNE word maps | `fig_tsne_freq.png`, `fig_tsne_tfidf.png` |
| Table A2: unsupervised LDA | `lda_summary.csv` |
| Table A3: seed dictionary | `seed_paragraph_counts.csv` |
| Table A4: seeded topics and their stability across 100 fits | `stability_seeded_topics.csv`, `seeded_topic_prevalence.csv` |
| Table A5: where unseeded words land across 100 fits | `stability_word_landing.csv` |
| Gender test | `gender_topic_words.csv` |
| Choice of k; robustness | `k_selection.csv`; `robustness.csv` |

All results come from one final run. An earlier full run produced byte-for-byte identical data files; only the label placement in the t-SNE figures differs. Package versions are printed at the end of the R Markdown file. Requires R (≥ 4.5).

## Data

306 long reviews (2005–2026) and 1,079 short comments from Douban, collected with [douban-reception-scraper](https://github.com/jiayizhang-k/douban-reception-scraper). **Review texts are not redistributed.** Many reviews discuss politically sensitive history, so the raw texts, user information, and review-level hand codes are kept private to protect reviewers. Reviews quoted in the paper are identified by their Douban review IDs. The files in `results/` contain no review text.

## Author

Jiayi Zhang, M.A. candidate in East Asian Studies, UCLA

## License

Code: MIT (see `LICENSE`). The license covers the code only, not the Douban review texts.
