# Writing Sample: Douban Reviews of *The Blue Kite*

Analysis code and results for my writing sample on how Chinese viewers interpret *The Blue Kite* (蓝风筝, dir. Tian Zhuangzhuang, 1993), a film banned in mainland China that follows one family through the Anti-Rightist Campaign, the Great Leap Forward, and the Cultural Revolution.

**Research question.** How do viewers of *The Blue Kite* interpret the suffering it shows under the revolutionary order, and how do they construct competing explanations of its causes and of who bears responsibility?

## Data

- 306 Chinese-language long reviews (2005–2026) and 1,079 short comments from Douban, collected with [douban-reception-scraper](https://github.com/jiayizhang-k/douban-reception-scraper).
- **Review texts are not redistributed.** Many reviews discuss politically sensitive history, so the raw texts, user information, and review-level hand codes are kept private to protect reviewers. Reviews quoted in the paper are identified by their Douban review IDs. Everything in `outputs/` is derived at the level of words and topics and contains no review text.

## Pipeline

Computational methods are used to guide close reading, not to replace it.

1. **Preprocessing** (`quanteda`): Chinese word segmentation with character names kept as single tokens; standard and custom stopword lists; paragraphs as documents (1,989 paragraphs; paragraphs under 30 characters merged into the next); words used at least 5 times in at least 3 paragraphs.
2. **Exploratory maps** (`Rtsne`): t-SNE of the 80 most frequent and the 80 most distinctive (TF-IDF) words.
3. **Unsupervised LDA**: k = 8, chosen after comparing values of k from 4 to 15; 100 fits from different random starts.
4. **Seeded LDA** (`seededlda`): a seed dictionary of 7 topics, built from the exploratory models with explicit rules for each seed word, plus 3 residual topics; 100 fits. The possible outcomes of the gender test were stated in advance (section 9 of the code).
5. **Visualization** (`LDAvis`): intertopic distance maps.
6. **Close reading and hand coding**: every quoted review was read in full. Two coding schemes (the folk belief *kefu* and the attribution of responsibility) are described in the paper's appendix.

## Where to find the results in the paper

| Paper | File |
|---|---|
| Figure 1 (seeded LDA topic map) | `outputs/figures/LDAvis_seeded_standalone.html` (download and open in a browser) |
| Figures A1–A2 (t-SNE word maps) | `outputs/figures/fig_tsne_freq.png`, `fig_tsne_tfidf.png` |
| Table A1 (t-SNE clusters) | `outputs/tables/exploratory/tsne_*_clusters.csv` |
| Table A2 (unsupervised LDA) | `outputs/tables/unsupervised_lda/lda_summary.csv` |
| Table A3 (seed dictionary) | `outputs/tables/seeded_lda/seed_paragraph_counts.csv` |
| Table A4 (seeded topics and their stability across 100 fits) | `outputs/tables/seeded_lda/stability_seeded_topics.csv`, `seeded_topic_prevalence.csv` |
| Table A5 (where unseeded words land across 100 fits) | `outputs/tables/seeded_lda/stability_word_landing.csv` |
| Gender test | `outputs/tables/gender_test/` |
| Choice of k; robustness checks | `outputs/tables/unsupervised_lda/k_selection.csv`; `outputs/tables/robustness/` |

## Code map

`analysis/blue_kite_analysis.Rmd`, by section:

| Section | Contents |
|---|---|
| 0–2 | Packages; loading and cleaning; tokenization and stopwords |
| 3–4 | Word counts and collocates (the mother, women, *kefu*) |
| 5 | Export of *kefu* passages for hand coding |
| 6 | Paragraph corpus and document-feature matrix |
| 7 | t-SNE maps and figures |
| 8 | Unsupervised LDA: choosing k, 100 fits, most typical fit, stability |
| 9 | Seeded LDA: seed rules, 100 fits, stability, the gender test |
| 10 | Where key unseeded words land |
| 11 | Robustness: random starts, residual topics, alternative dictionaries, review-level model |
| 12 | LDAvis topic map |

## Reproducibility

All results come from one final run of the code. An earlier full run produced byte-for-byte identical data files; only the label placement in the t-SNE figures differs, because labels are positioned at random. Package versions are printed in the session-info chunk at the end of the R Markdown file. Requires R (≥ 4.5).

## Author

Jiayi Zhang, M.A. candidate in East Asian Studies, UCLA
