# CLOUS: Cross-Linguistic Orthographic Uniqueness Score

[![Hugging Face Spaces](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Spaces-blue)](https://huggingface.co/spaces/ric-rivera/CLOUS-Tokenizer-Diagnostic)

An independent, exploratory research project investigating character-level orthographic rarity and its relationship to multilingual tokenization fragmentation.

## How This Started

This project began with a simple question:

> Which country name is the most unique?

“Unique” can mean many things. I chose one measurable interpretation: how uncommon a name’s individual characters are relative to a language-specific character-frequency profile.

That question led to CLOUS, a multilingual benchmark, and an investigation into whether character-level rarity is associated with how tokenizers split country names.

This was my first independent research project. The repository documents the resulting methodology, experiments, manuscript, and interactive application.

## What I Built

* A character-level scoring metric based on mean Shannon surprisal.
* A dataset of 249 ISO-listed country and territory entries localized across eleven languages using Unicode CLDR.
* Language-specific character-frequency profiles derived from Leipzig corpora.
* A Python evaluation pipeline comparing CLOUS with tokenization results from six tokenizers.
* Statistical comparisons against character count, UTF-8 byte length, and character-bigram surprisal.
* A research manuscript documenting the methods, results, interpretations, and limitations.
* An interactive Hugging Face application for exploring scores and tokenizer outputs.

The project spans question formulation, data preparation, metric design, statistical evaluation, visualization, research writing, and application development.

## What CLOUS Measures

CLOUS computes the average surprisal of the characters in an NFC-normalized string using a selected language’s character-frequency profile.

Higher scores indicate that the string contains characters that are less common in that reference corpus.

CLOUS measures character-level orthographic rarity. It does not measure:

* Cultural or semantic uniqueness.
* How familiar a complete name is to a language model.
* Whether a model understands an entity correctly.
* The probability of hallucination or downstream task failure.

Because the score uses individual character frequencies, it does not account for character order. Strings with the same character composition receive the same CLOUS score under the same frequency profile.

## Study Scope

The manuscript evaluates:

* 249 country and territory entries.
* Eleven languages.
* Six tokenizers: GPT-4, GPT-4o, Llama 3, Gemma, mBERT, and XLM-R.
* 65 valid language–tokenizer correlation tests, with one constant-output combination excluded.

Fragmentation is operationalized as character-normalized fertility:

    fertility = output token count / input character count

This differs from word-level fertility measures. Results should be interpreted using the denominator defined here.

## Findings Reported in the Manuscript

Within the evaluated benchmark:

* CLOUS was significantly associated with character-normalized fertility in 61 of 65 valid language–tokenizer combinations after Benjamini–Hochberg correction.
* Associations were generally stronger for non-Latin scripts than for Latin-script languages.
* CLOUS had a higher Spearman correlation than the character-bigram baseline in 45 of 65 combinations.
* A pooled screening analysis reported ROC-AUC = 0.850 and F1 = 0.740 for identifying the highest-fertility quartile.

These are results reported for this benchmark, not independently validated performance guarantees for new inputs.

The manuscript also compares CLOUS with length-based measures. Those comparisons require caution: character count is the denominator of the fertility outcome, and negative baseline correlations should not automatically be interpreted as weaker predictive performance.

## Research Status and Limitations

This is independent exploratory work. It has not been peer-reviewed or formally published.

Important boundaries include:

* The main benchmark consists of country and territory names. Generalization to person names, organizations, addresses, or arbitrary text has not been established.
* Character-frequency profiles depend on the selected corpus and may differ across domains and writing styles.
* Correlation does not establish causation.
* Pooled results may conceal differences between languages and tokenizers.
* The manuscript does not document held-out validation of the reported screening performance.
* Universal score thresholds and individualized token-cost predictions have not been established.
* Lower token counts alone do not establish better model understanding or downstream performance.

The repository is shared to make the approach inspectable, support reproduction, and invite methodological feedback.

## 🚀 Interactive Application

[Explore CLOUS on Hugging Face](https://huggingface.co/spaces/ric-rivera/CLOUS-Tokenizer-Diagnostic)

The application lets users select a language profile, calculate a CLOUS score, and inspect tokenization outputs across the evaluated tokenizers.

Users can enter strings beyond the original benchmark, but those inputs fall outside the study’s validated scope.

Any risk labels or quartile-based messages in the application should be treated as exploratory benchmark-based indicators—not calibrated predictions for an individual input. In particular, the reported difference between benchmark quartiles does not establish an expected percentage increase for a newly entered name.

## Illustrative Example: Arabic Typography

The manuscript examines variations of the Arabic name for Córdoba, including the addition of diacritics and typographical elongation characters.

These examples illustrate how orthographic changes can alter both character-rarity scores and tokenizer outputs. They are case studies, not independent validation of CLOUS across arbitrary typography or named entities.

See the manuscript for the tested strings and reported token counts.

## Repository Structure

* `raw_corpora/`: Leipzig character and word frequency files used to construct reference profiles.
* `cache/`: Serialized frequency maps and intermediate outputs, including `benchmark_results.csv`, `final_stats.csv`, and `clous_scores.csv`.
* `CLOUS_pipeline.ipynb`: Main evaluation notebook.
* `results/`: Generated figures and benchmark outputs.
* `Rivera_2026_CLOUS_Tokenization_V6.pdf`: Research manuscript.

## Reproducing the Analysis

1. Download the required Leipzig Corpora Collection frequency files from [Wortschatz Leipzig](https://wortschatz.uni-leipzig.de/en/download).
2. Place the character-frequency (`_letters.txt`) and word-frequency (`_words.txt`) files in `raw_corpora/`.
3. Use the target locales: `en`, `es`, `fr`, `ru`, `ar`, `hi`, `zh-Hans`, `ja`, `ta`, `tr`, and `ko`.
4. Open `CLOUS_pipeline.ipynb` in Google Colab or a local Jupyter environment.
5. Ensure the expected data and cache directories are accessible.
6. Run the notebook cells sequentially to construct profiles, compute scores, tokenize entities, and generate statistical comparisons.

Consult the notebook for dependencies, tokenizer configuration, and input-file requirements.

## Potential Next Steps

* Held-out evaluation on unseen entities.
* Language-specific screening thresholds and uncertainty estimates.
* More rigorous comparisons with length-based and n-gram baselines.
* Separate evaluation on other named-entity types.
* Tests of whether fragmentation differences correspond to downstream performance or practical cost differences.

These are possible extensions, not completed results.

## Citation

If you use the metric, code, or benchmark in your work, please cite the independent manuscript and identify the repository version or commit used.

```bibtex
@misc{rivera2026clous,
  title = {Estimating Cross-Lingual Tokenization Fragmentation Risk: A Frequency-Based Uniqueness Score for Geographic Entities},
  author = {Rivera, Richard},
  year = {2026},
  howpublished = {GitHub repository},
  url = {[https://github.com/ric-rivera/CLOUS-tokenization-metrics](https://github.com/ric-rivera/CLOUS-tokenization-metrics)},
  note = {Independent research manuscript; not peer-reviewed}
}
```
