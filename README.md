# Writing Sample: Douban Reviews of *The Blue Kite*

Analysis code for my writing sample on how Chinese viewers interpret *The Blue Kite* (蓝风筝, dir. Tian Zhuangzhuang, 1993), a film banned in mainland China that follows one family through the Anti-Rightist Campaign, the Great Leap Forward, and the Cultural Revolution.

**Research question.** How do viewers of *The Blue Kite* interpret the suffering it shows under the revolutionary order, and how do they construct competing explanations of its causes and of who bears responsibility?

## Data

- 306 Chinese-language long reviews (2005–2026) and 1,079 short comments from Douban, collected with [douban-reception-scraper](https://github.com/jiayizhang-k/douban-reception-scraper).
- **Review texts are not redistributed.** Many reviews discuss politically sensitive history, so the raw texts and user information are kept private to protect reviewers. Reviews quoted in the paper are identified by their Douban review IDs.

## Pipeline

Computational methods are used to guide close reading, not to replace it.

1. **Preprocessing** (`quanteda`): Chinese word segmentation with character names kept as single tokens; standard and custom stopword lists; paragraphs as documents (1,989 paragraphs; paragraphs under 30 characters merged into the next); words used at least 5 times in at least 3 paragraphs.
2. **Exploratory maps** (`Rtsne`): t-SNE of the 80 most frequent and the 80 most distinctive (TF-IDF) words.
3. **Unsupervised LDA**: k = 8, chosen after comparing 4–15 topics; 100 fits from different random starts.
4. **Seeded LDA** (`seededlda`): a seed dictionary of 7 topics, built from the exploratory models with explicit rules for each seed word, plus 3 residual topics; 100 fits, with topic stability and the placement of unseeded words reported across fits.
5. **Visualization** (`LDAvis`): intertopic distance map of the seeded model.
6. **Close reading and hand coding**: every quoted review was read in full. Two coding schemes (the folk belief *kefu* and the attribution of responsibility) are described in the paper's appendix.

## Files

| Path | Contents |
|---|---|
| `analysis/blue_kite_analysis.Rmd` | Full analysis: preprocessing, t-SNE, unsupervised and seeded LDA, stability checks, figures |

## Requirements

R (≥ 4.5). Package list in the setup chunk of the R Markdown file.

## Author

Jiayi Zhang, M.A. candidate in East Asian Studies, UCLA
