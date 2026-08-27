# Calm is the angriest app in its category, and almost none of it is about meditation

A positioning and messaging analysis for **Calm**, benchmarked against Headspace,
Intellect and 48 other apps, built by mining 200,972 Google Play reviews of 73 mental
health apps and comparing them against archive-verified marketing copy from the same
years.

**Read the case study:** https://isha-das-06.github.io/say-do-gap/

## The finding

Calm ranks **first of 51** apps on the share of its negative reviews that are about
money and access, at 65.0% against a category median of 18.2%. 53.5% of its detractors
complain only about money and access, with no product complaint at all; 10.1% complain
only about the product.

Meanwhile sleep is named in 41.2% of its positive reviews, more than double Headspace's
19.2%. The product promise holds. The commercial experience does not.

Between 2019 and 2022 the complaint also changed character: price complaints fell from
32.5% of detractors to 16.1%, while "everything is locked" rose from 19.3% to 32.5%.
That is a packaging problem, not a pricing problem, which is why discounting would not
fix it. And 7.3% of Calm's detractors name a free audio substitute, YouTube most often,
so the competitive frame is Calm against free rather than Calm against Headspace.

## Data

[MHARD — Mental Health App Reviews Dataset](https://github.com/Sensify-Lab/MHARD),
200,972 reviews of 73 mental health apps with 100k+ downloads, posted 29 March 2011
to 11 July 2023, collected via SerpAPI. MIT licensed.
Paper: [Wang et al., ICWSM 2025](https://doi.org/10.1609/icwsm.v19i1.35916) ·
Archive: [Zenodo](https://doi.org/10.5281/zenodo.22863690)

Marketing claims come from Internet Archive snapshots of calm.com, headspace.com and
their Google Play listings, June 2021 to June 2023, so both halves of the say-do
comparison are dated inside the same window. Sourcing is in `research/`.

## Method

1. **Discovery.** Non-negative matrix factorisation over TF-IDF vectors of the review
   text, unsupervised, to find what the corpus is about before imposing assumptions.
2. **Measurement.** The discovered topics become a dictionary of 16 labelled regular
   expressions, applied multi-label. A dictionary is auditable; a black-box cluster
   assignment is not. Sampled precision is around 90%.
3. **External check.** Cerebral, an app the FTC sued in April 2024 over cancellation
   practices, ranks first of all apps on the dictionary's cancellation measure at 32.0%
   without being singled out. One case, not a formal validation, but the right check to
   run before acting on the numbers.
4. **Comparison.** Measured theme frequencies set against archived, date-matched
   marketing claims.

## Reproducing it

```bash
pip install pandas numpy scikit-learn matplotlib jupyter
jupyter notebook notebook/app_review_mining_calm_positioning.ipynb
```

The notebook downloads the dataset itself on first run (~79 MB) and executes top to
bottom with no errors. Every figure on the site and in this README comes out of it.

## Limitations

Google Play only, no App Store. Dictionary measurement understates complaints phrased
in wording the rules miss, so every figure is a floor. Reviewers are a self-selecting,
disproportionately annoyed sample and say nothing about users who quietly stopped
opening the app. The recommendation is a reasoned hypothesis with no experiment behind
it. Calm's monthly price rose from $12.99 to $14.99 after the review window closed.
Full list on the site.

## Repository

```
index.html                                            the case study (Pages entry point)
notebook/app_review_mining_calm_positioning.ipynb     full reproducible analysis
research/                                             sourcing for every marketing claim
```

The page is a single self-contained HTML file. All eight charts are inline SVG with no
JavaScript library and no CDN dependency, so it renders offline and will not break when
a CDN changes.

## Licence

Analysis and write-up © 2026 Isha Das, MIT. The MHARD dataset is MIT licensed by its
authors and is not redistributed here. Marketing copy quoted is the property of the
respective companies and is reproduced for commentary and criticism.
