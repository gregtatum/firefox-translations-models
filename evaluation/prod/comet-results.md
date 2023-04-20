# What is COMET

COMET is a neural framework its developers present for training multilingual machine translation evaluation models. The framework has been reported to obtain new state-of-the-art levels of correlation with human judgments. Recent breakthroughs in cross-lingual pre-trained language modeling have been leveraged by the framework resulting in highly multilingual and adaptable MT evaluation models.

Three models with different human judgments have been trained to showcase the framework. These include Direct Assessments, Human-mediated Translation Edit Rate, and Multidimensional Quality Metrics. These models are designed to exploit information from source input and a target-language reference translation to more accurately predict MT quality.

The models developed by COMET have achieved new state-of-the-art performance on the WMT 2019 Metrics shared task, demonstrating robustness to high-performing systems.

Source: https://aclanthology.org/2020.emnlp-main.213.pdf

Tool: https://github.com/Unbabel/COMET

# What are these benchmarks

## Translators

1. **bergamot** - uses compiled  [bergamot-translator](https://github.com/mozilla/bergamot-translator)  (wrapper for marian that is used by Firefox Translations web extension)
2. **google** - uses Google Translation [API](https://cloud.google.com/translate)
3. **microsoft** - uses Azure Cognitive Services Translator [API](https://azure.microsoft.com/en-us/services/cognitive-services/translator/)

## Method

We use official WMT ([Conference on Machine Translation](http://statmt.org/wmt21/)) parallel datasets. Available datasets are discovered automatically based on a language pair.

We perform the translation from source to target language using one of the three translation systems, compare the result with the dataset reference, and then calculate the [COMET](https://github.com/Unbabel/COMET) score.

Both absolute and relative differences in the scores between Bergamot and other systems are reported.

We also compare the systems using the `comet-compare` tool that calculates the statistical significance with Paired T-Test and bootstrap resampling.

# Evaluation results

`avg` = average on all datasets



## avg

| Translator/Dataset | en-pt | pt-en | en-bg | nb-en | it-en | en-et | fr-en | en-de | es-en | en-it | en-pl | en-es | pl-en | en-fr | et-en | bg-en | de-en | en-cs | cs-en |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| bergamot | 0.86 | 0.75 | 0.80 | 0.64 | 0.62 | 0.86 | 0.59 | 0.51 | 0.55 | 0.68 | 0.66 | 0.61 | 0.56 | 0.56 | 0.60 | 0.68 | 0.49 | 0.61 | 0.48 |
| google | 0.93 (+0.06, +7.42%) | 0.80 (+0.05, +6.85%) | 0.88 (+0.09, +10.75%) | 0.81 (+0.17, +26.28%) | 0.68 (+0.06, +10.18%) | 1.07 (+0.21, +24.57%) | 0.65 (+0.06, +10.69%) | 0.60 (+0.09, +17.91%) | 0.62 (+0.07, +11.99%) | 0.76 (+0.08, +12.35%) | 0.82 (+0.17, +25.52%) | 0.69 (+0.09, +14.08%) | 0.66 (+0.09, +16.81%) | 0.67 (+0.11, +20.19%) | 0.77 (+0.17, +28.18%) | 0.75 (+0.07, +10.49%) | 0.61 (+0.11, +22.99%) | 0.83 (+0.22, +35.44%) | 0.61 (+0.13, +26.78%) |
| microsoft | 0.91 (+0.05, +5.54%) | 0.79 (+0.05, +6.20%) | 0.86 (+0.07, +8.17%) | 0.81 (+0.16, +25.57%) | 0.68 (+0.06, +10.18%) | 1.05 (+0.19, +22.64%) | 0.67 (+0.08, +13.12%) | 0.61 (+0.10, +20.20%) | 0.63 (+0.08, +13.82%) | 0.76 (+0.09, +12.87%) | 0.80 (+0.14, +21.56%) | 0.70 (+0.09, +14.92%) | 0.66 (+0.10, +17.36%) | 0.69 (+0.13, +23.23%) | 0.74 (+0.14, +23.46%) | 0.73 (+0.05, +7.05%) | 0.63 (+0.13, +26.85%) | 0.84 (+0.23, +37.82%) | 0.62 (+0.14, +27.97%) |

![Results](img/avg-comet.png)
---

## en-pt

| Translator/Dataset | flores-dev | flores-test |
| --- | --- | --- |
| bergamot | 0.87 | 0.86 |
| google | 0.93 (+0.06, +7.41%) | 0.92 (+0.06, +7.44%) |
| microsoft | 0.91 (+0.04, +4.89%) | 0.91 (+0.05, +6.19%) |

![Results](img/en-pt-comet.png)
### Comparisons between systems
*If a comparison is omitted, the systems have equal averages (tie). Click on the dataset for a complete report*
#### [flores-dev.en-pt](en-pt/flores-dev.en-pt.cometcompare)
- flores-dev.microsoft.pt outperforms flores-dev.bergamot.pt.
- flores-dev.google.pt outperforms flores-dev.bergamot.pt.
- flores-dev.google.pt outperforms flores-dev.microsoft.pt.

#### [flores-test.en-pt](en-pt/flores-test.en-pt.cometcompare)
- flores-test.microsoft.pt outperforms flores-test.bergamot.pt.
- flores-test.google.pt outperforms flores-test.bergamot.pt.
- flores-test.google.pt outperforms flores-test.microsoft.pt.

---

## pt-en

| Translator/Dataset | flores-dev | flores-test | mtedx_test |
| --- | --- | --- | --- |
| bergamot | 0.81 | 0.80 | 0.63 |
| google | 0.85 (+0.04, +4.40%) | 0.85 (+0.05, +6.39%) | 0.70 (+0.07, +10.56%) |
| microsoft | 0.84 (+0.03, +4.17%) | 0.85 (+0.05, +6.39%) | 0.69 (+0.05, +8.54%) |

![Results](img/pt-en-comet.png)
### Comparisons between systems
*If a comparison is omitted, the systems have equal averages (tie). Click on the dataset for a complete report*
#### [flores-dev.pt-en](pt-en/flores-dev.pt-en.cometcompare)
- flores-dev.microsoft.en outperforms flores-dev.bergamot.en.
- flores-dev.google.en outperforms flores-dev.bergamot.en.

#### [flores-test.pt-en](pt-en/flores-test.pt-en.cometcompare)
- flores-test.microsoft.en outperforms flores-test.bergamot.en.
- flores-test.google.en outperforms flores-test.bergamot.en.

#### [mtedx_test.pt-en](pt-en/mtedx_test.pt-en.cometcompare)
- mtedx_test.microsoft.en outperforms mtedx_test.bergamot.en.
- mtedx_test.google.en outperforms mtedx_test.bergamot.en.
- mtedx_test.google.en outperforms mtedx_test.microsoft.en.

---

## en-bg

| Translator/Dataset | flores-test | flores-dev |
| --- | --- | --- |
| bergamot | 0.80 | 0.79 |
| google | 0.89 (+0.09, +10.78%) | 0.88 (+0.09, +10.71%) |
| microsoft | 0.87 (+0.07, +8.38%) | 0.86 (+0.06, +7.95%) |

![Results](img/en-bg-comet.png)
### Comparisons between systems
*If a comparison is omitted, the systems have equal averages (tie). Click on the dataset for a complete report*
#### [flores-test.en-bg](en-bg/flores-test.en-bg.cometcompare)
- flores-test.microsoft.bg outperforms flores-test.bergamot.bg.
- flores-test.google.bg outperforms flores-test.bergamot.bg.
- flores-test.google.bg outperforms flores-test.microsoft.bg.

#### [flores-dev.en-bg](en-bg/flores-dev.en-bg.cometcompare)
- flores-dev.microsoft.bg outperforms flores-dev.bergamot.bg.
- flores-dev.google.bg outperforms flores-dev.bergamot.bg.
- flores-dev.google.bg outperforms flores-dev.microsoft.bg.

---

## nb-en

| Translator/Dataset | flores-dev | flores-test |
| --- | --- | --- |
| bergamot | 0.64 | 0.65 |
| google | 0.81 (+0.18, +27.71%) | 0.81 (+0.16, +24.86%) |
| microsoft | 0.81 (+0.17, +26.75%) | 0.80 (+0.16, +24.41%) |

![Results](img/nb-en-comet.png)
### Comparisons between systems
*If a comparison is omitted, the systems have equal averages (tie). Click on the dataset for a complete report*
#### [flores-dev.nb-en](nb-en/flores-dev.nb-en.cometcompare)
- flores-dev.microsoft.en outperforms flores-dev.bergamot.en.
- flores-dev.google.en outperforms flores-dev.bergamot.en.
- flores-dev.google.en outperforms flores-dev.microsoft.en.

#### [flores-test.nb-en](nb-en/flores-test.nb-en.cometcompare)
- flores-test.microsoft.en outperforms flores-test.bergamot.en.
- flores-test.google.en outperforms flores-test.bergamot.en.

---

## it-en

| Translator/Dataset | flores-dev | flores-test | mtedx_test | wmt09 |
| --- | --- | --- | --- | --- |
| bergamot | 0.72 | 0.70 | 0.55 | 0.53 |
| google | 0.76 (+0.04, +6.00%) | 0.76 (+0.06, +9.33%) | 0.62 (+0.07, +12.79%) | 0.60 (+0.08, +14.29%) |
| microsoft | 0.76 (+0.04, +6.16%) | 0.76 (+0.06, +8.80%) | 0.61 (+0.06, +11.31%) | 0.61 (+0.09, +16.28%) |

![Results](img/it-en-comet.png)
### Comparisons between systems
*If a comparison is omitted, the systems have equal averages (tie). Click on the dataset for a complete report*
#### [flores-dev.it-en](it-en/flores-dev.it-en.cometcompare)
- flores-dev.microsoft.en outperforms flores-dev.bergamot.en.
- flores-dev.google.en outperforms flores-dev.bergamot.en.

#### [flores-test.it-en](it-en/flores-test.it-en.cometcompare)
- flores-test.microsoft.en outperforms flores-test.bergamot.en.
- flores-test.google.en outperforms flores-test.bergamot.en.

#### [mtedx_test.it-en](it-en/mtedx_test.it-en.cometcompare)
- mtedx_test.microsoft.en outperforms mtedx_test.bergamot.en.
- mtedx_test.google.en outperforms mtedx_test.bergamot.en.

#### [wmt09.it-en](it-en/wmt09.it-en.cometcompare)
- wmt09.microsoft.en outperforms wmt09.bergamot.en.
- wmt09.google.en outperforms wmt09.bergamot.en.
- wmt09.microsoft.en outperforms wmt09.google.en.

---

## en-et

| Translator/Dataset | wmt18 | flores-test | flores-dev |
| --- | --- | --- | --- |
| bergamot | 0.83 | 0.87 | 0.86 |
| google | 1.03 (+0.20, +23.75%) | 1.07 (+0.20, +23.56%) | 1.09 (+0.23, +26.39%) |
| microsoft | 1.02 (+0.18, +22.12%) | 1.07 (+0.20, +23.04%) | 1.06 (+0.20, +22.76%) |

![Results](img/en-et-comet.png)
### Comparisons between systems
*If a comparison is omitted, the systems have equal averages (tie). Click on the dataset for a complete report*
#### [wmt18.en-et](en-et/wmt18.en-et.cometcompare)
- wmt18.microsoft.et outperforms wmt18.bergamot.et.
- wmt18.google.et outperforms wmt18.bergamot.et.
- wmt18.google.et outperforms wmt18.microsoft.et.

#### [flores-test.en-et](en-et/flores-test.en-et.cometcompare)
- flores-test.microsoft.et outperforms flores-test.bergamot.et.
- flores-test.google.et outperforms flores-test.bergamot.et.

#### [flores-dev.en-et](en-et/flores-dev.en-et.cometcompare)
- flores-dev.microsoft.et outperforms flores-dev.bergamot.et.
- flores-dev.google.et outperforms flores-dev.bergamot.et.
- flores-dev.google.et outperforms flores-dev.microsoft.et.

---

## fr-en

| Translator/Dataset | wmt13 | iwslt17 | wmt10 | wmt14 | wmt11 | flores-dev | flores-test | wmt15 | wmt08 | mtedx_test | wmt12 | wmt09 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| bergamot | 0.58 | 0.67 | 0.53 | 0.64 | 0.51 | 0.77 | 0.77 | 0.56 | 0.44 | 0.62 | 0.50 | 0.50 |
| google | 0.63 (+0.04, +7.32%) | 0.71 (+0.04, +5.84%) | 0.61 (+0.08, +15.85%) | 0.71 (+0.06, +9.51%) | 0.57 (+0.06, +11.60%) | 0.82 (+0.05, +6.94%) | 0.82 (+0.05, +6.04%) | 0.66 (+0.10, +17.10%) | 0.52 (+0.09, +19.65%) | 0.69 (+0.07, +11.22%) | 0.55 (+0.05, +10.25%) | 0.57 (+0.07, +13.97%) |
| microsoft | 0.65 (+0.07, +11.46%) | 0.73 (+0.06, +8.36%) | 0.63 (+0.10, +18.76%) | 0.72 (+0.08, +12.36%) | 0.60 (+0.09, +17.14%) | 0.82 (+0.05, +7.03%) | 0.82 (+0.05, +6.45%) | 0.66 (+0.10, +17.71%) | 0.53 (+0.10, +22.35%) | 0.69 (+0.07, +11.77%) | 0.58 (+0.08, +16.77%) | 0.58 (+0.08, +16.90%) |

![Results](img/fr-en-comet.png)
### Comparisons between systems
*If a comparison is omitted, the systems have equal averages (tie). Click on the dataset for a complete report*
#### [wmt13.fr-en](fr-en/wmt13.fr-en.cometcompare)
- wmt13.microsoft.en outperforms wmt13.bergamot.en.
- wmt13.google.en outperforms wmt13.bergamot.en.
- wmt13.microsoft.en outperforms wmt13.google.en.

#### [iwslt17.fr-en](fr-en/iwslt17.fr-en.cometcompare)
- iwslt17.microsoft.en outperforms iwslt17.bergamot.en.
- iwslt17.google.en outperforms iwslt17.bergamot.en.
- iwslt17.microsoft.en outperforms iwslt17.google.en.

#### [wmt10.fr-en](fr-en/wmt10.fr-en.cometcompare)
- wmt10.microsoft.en outperforms wmt10.bergamot.en.
- wmt10.google.en outperforms wmt10.bergamot.en.
- wmt10.microsoft.en outperforms wmt10.google.en.

#### [wmt14.fr-en](fr-en/wmt14.fr-en.cometcompare)
- wmt14.microsoft.en outperforms wmt14.bergamot.en.
- wmt14.google.en outperforms wmt14.bergamot.en.
- wmt14.microsoft.en outperforms wmt14.google.en.

#### [wmt11.fr-en](fr-en/wmt11.fr-en.cometcompare)
- wmt11.microsoft.en outperforms wmt11.bergamot.en.
- wmt11.google.en outperforms wmt11.bergamot.en.
- wmt11.microsoft.en outperforms wmt11.google.en.

#### [flores-dev.fr-en](fr-en/flores-dev.fr-en.cometcompare)
- flores-dev.microsoft.en outperforms flores-dev.bergamot.en.
- flores-dev.google.en outperforms flores-dev.bergamot.en.

#### [flores-test.fr-en](fr-en/flores-test.fr-en.cometcompare)
- flores-test.microsoft.en outperforms flores-test.bergamot.en.
- flores-test.google.en outperforms flores-test.bergamot.en.

#### [wmt15.fr-en](fr-en/wmt15.fr-en.cometcompare)
- wmt15.microsoft.en outperforms wmt15.bergamot.en.
- wmt15.google.en outperforms wmt15.bergamot.en.

#### [wmt08.fr-en](fr-en/wmt08.fr-en.cometcompare)
- wmt08.microsoft.en outperforms wmt08.bergamot.en.
- wmt08.google.en outperforms wmt08.bergamot.en.
- wmt08.microsoft.en outperforms wmt08.google.en.

#### [mtedx_test.fr-en](fr-en/mtedx_test.fr-en.cometcompare)
- mtedx_test.microsoft.en outperforms mtedx_test.bergamot.en.
- mtedx_test.google.en outperforms mtedx_test.bergamot.en.

#### [wmt12.fr-en](fr-en/wmt12.fr-en.cometcompare)
- wmt12.microsoft.en outperforms wmt12.bergamot.en.
- wmt12.google.en outperforms wmt12.bergamot.en.
- wmt12.microsoft.en outperforms wmt12.google.en.

#### [wmt09.fr-en](fr-en/wmt09.fr-en.cometcompare)
- wmt09.microsoft.en outperforms wmt09.bergamot.en.
- wmt09.google.en outperforms wmt09.bergamot.en.
- wmt09.microsoft.en outperforms wmt09.google.en.

---

## en-de

| Translator/Dataset | wmt12 | wmt16 | wmt15 | flores-dev | wmt21 | wmt17 | wmt10 | flores-test | wmt08 | wmt18 | wmt22 | wmt20 | wmt19 | wmt09 | wmt11 | wmt13 | wmt14 | iwslt17 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| bergamot | 0.43 | 0.60 | 0.54 | 0.60 | 0.46 | 0.55 | 0.49 | 0.62 | 0.42 | 0.65 | 0.46 | 0.50 | 0.55 | 0.43 | 0.41 | 0.51 | 0.55 | 0.43 |
| google | 0.52 (+0.08, +19.17%) | 0.67 (+0.08, +12.64%) | 0.64 (+0.10, +17.92%) | 0.70 (+0.09, +15.43%) | 0.52 (+0.06, +14.16%) | 0.64 (+0.09, +16.72%) | 0.57 (+0.07, +15.28%) | 0.70 (+0.09, +14.23%) | 0.52 (+0.10, +24.24%) | 0.72 (+0.07, +10.80%) | 0.62 (+0.16, +34.59%) | 0.60 (+0.10, +19.53%) | 0.62 (+0.07, +13.58%) | 0.53 (+0.10, +22.21%) | 0.50 (+0.10, +24.37%) | 0.59 (+0.08, +15.78%) | 0.66 (+0.10, +18.81%) | 0.52 (+0.10, +22.49%) |
| microsoft | 0.54 (+0.10, +23.89%) | 0.69 (+0.09, +15.21%) | 0.64 (+0.10, +18.87%) | 0.70 (+0.09, +15.61%) | 0.55 (+0.09, +19.86%) | 0.64 (+0.10, +18.33%) | 0.59 (+0.10, +19.38%) | 0.71 (+0.09, +14.73%) | 0.54 (+0.12, +27.31%) | 0.73 (+0.08, +12.41%) | 0.63 (+0.17, +36.02%) | 0.61 (+0.11, +22.10%) | 0.64 (+0.09, +16.54%) | 0.54 (+0.11, +25.27%) | 0.52 (+0.12, +29.30%) | 0.60 (+0.09, +18.10%) | 0.66 (+0.11, +19.77%) | 0.52 (+0.10, +22.70%) |

![Results](img/en-de-comet.png)
### Comparisons between systems
*If a comparison is omitted, the systems have equal averages (tie). Click on the dataset for a complete report*
#### [wmt12.en-de](en-de/wmt12.en-de.cometcompare)
- wmt12.microsoft.de outperforms wmt12.bergamot.de.
- wmt12.google.de outperforms wmt12.bergamot.de.
- wmt12.microsoft.de outperforms wmt12.google.de.

#### [wmt16.en-de](en-de/wmt16.en-de.cometcompare)
- wmt16.microsoft.de outperforms wmt16.bergamot.de.
- wmt16.google.de outperforms wmt16.bergamot.de.
- wmt16.microsoft.de outperforms wmt16.google.de.

#### [wmt15.en-de](en-de/wmt15.en-de.cometcompare)
- wmt15.microsoft.de outperforms wmt15.bergamot.de.
- wmt15.google.de outperforms wmt15.bergamot.de.

#### [flores-dev.en-de](en-de/flores-dev.en-de.cometcompare)
- flores-dev.microsoft.de outperforms flores-dev.bergamot.de.
- flores-dev.google.de outperforms flores-dev.bergamot.de.

#### [wmt21.en-de](en-de/wmt21.en-de.cometcompare)
- wmt21.microsoft.de outperforms wmt21.bergamot.de.
- wmt21.google.de outperforms wmt21.bergamot.de.
- wmt21.microsoft.de outperforms wmt21.google.de.

#### [wmt17.en-de](en-de/wmt17.en-de.cometcompare)
- wmt17.microsoft.de outperforms wmt17.bergamot.de.
- wmt17.google.de outperforms wmt17.bergamot.de.
- wmt17.microsoft.de outperforms wmt17.google.de.

#### [wmt10.en-de](en-de/wmt10.en-de.cometcompare)
- wmt10.microsoft.de outperforms wmt10.bergamot.de.
- wmt10.google.de outperforms wmt10.bergamot.de.
- wmt10.microsoft.de outperforms wmt10.google.de.

#### [flores-test.en-de](en-de/flores-test.en-de.cometcompare)
- flores-test.microsoft.de outperforms flores-test.bergamot.de.
- flores-test.google.de outperforms flores-test.bergamot.de.

#### [wmt08.en-de](en-de/wmt08.en-de.cometcompare)
- wmt08.microsoft.de outperforms wmt08.bergamot.de.
- wmt08.google.de outperforms wmt08.bergamot.de.
- wmt08.microsoft.de outperforms wmt08.google.de.

#### [wmt18.en-de](en-de/wmt18.en-de.cometcompare)
- wmt18.microsoft.de outperforms wmt18.bergamot.de.
- wmt18.google.de outperforms wmt18.bergamot.de.
- wmt18.microsoft.de outperforms wmt18.google.de.

#### [wmt22.en-de](en-de/wmt22.en-de.cometcompare)
- wmt22.microsoft.de outperforms wmt22.bergamot.de.
- wmt22.google.de outperforms wmt22.bergamot.de.

#### [wmt20.en-de](en-de/wmt20.en-de.cometcompare)
- wmt20.microsoft.de outperforms wmt20.bergamot.de.
- wmt20.google.de outperforms wmt20.bergamot.de.
- wmt20.microsoft.de outperforms wmt20.google.de.

#### [wmt19.en-de](en-de/wmt19.en-de.cometcompare)
- wmt19.microsoft.de outperforms wmt19.bergamot.de.
- wmt19.google.de outperforms wmt19.bergamot.de.
- wmt19.microsoft.de outperforms wmt19.google.de.

#### [wmt09.en-de](en-de/wmt09.en-de.cometcompare)
- wmt09.microsoft.de outperforms wmt09.bergamot.de.
- wmt09.google.de outperforms wmt09.bergamot.de.
- wmt09.microsoft.de outperforms wmt09.google.de.

#### [wmt11.en-de](en-de/wmt11.en-de.cometcompare)
- wmt11.microsoft.de outperforms wmt11.bergamot.de.
- wmt11.google.de outperforms wmt11.bergamot.de.
- wmt11.microsoft.de outperforms wmt11.google.de.

#### [wmt13.en-de](en-de/wmt13.en-de.cometcompare)
- wmt13.microsoft.de outperforms wmt13.bergamot.de.
- wmt13.google.de outperforms wmt13.bergamot.de.
- wmt13.microsoft.de outperforms wmt13.google.de.

#### [wmt14.en-de](en-de/wmt14.en-de.cometcompare)
- wmt14.microsoft.de outperforms wmt14.bergamot.de.
- wmt14.google.de outperforms wmt14.bergamot.de.
- wmt14.microsoft.de outperforms wmt14.google.de.

#### [iwslt17.en-de](en-de/iwslt17.en-de.cometcompare)
- iwslt17.microsoft.de outperforms iwslt17.bergamot.de.
- iwslt17.google.de outperforms iwslt17.bergamot.de.

---

## es-en

| Translator/Dataset | wmt13 | wmt10 | wmt11 | flores-dev | flores-test | wmt08 | mtedx_test | wmt12 | wmt09 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| bergamot | 0.60 | 0.58 | 0.52 | 0.66 | 0.66 | 0.46 | 0.43 | 0.56 | 0.47 |
| google | 0.65 (+0.05, +7.48%) | 0.65 (+0.07, +11.52%) | 0.57 (+0.04, +8.52%) | 0.74 (+0.08, +12.89%) | 0.74 (+0.08, +12.52%) | 0.52 (+0.06, +12.89%) | 0.53 (+0.09, +21.84%) | 0.61 (+0.04, +7.32%) | 0.55 (+0.07, +15.87%) |
| microsoft | 0.67 (+0.07, +10.80%) | 0.66 (+0.07, +12.86%) | 0.60 (+0.07, +14.17%) | 0.73 (+0.07, +11.07%) | 0.73 (+0.07, +11.40%) | 0.53 (+0.07, +14.99%) | 0.54 (+0.11, +24.18%) | 0.63 (+0.07, +11.90%) | 0.55 (+0.08, +17.25%) |

![Results](img/es-en-comet.png)
### Comparisons between systems
*If a comparison is omitted, the systems have equal averages (tie). Click on the dataset for a complete report*
#### [wmt13.es-en](es-en/wmt13.es-en.cometcompare)
- wmt13.microsoft.en outperforms wmt13.bergamot.en.
- wmt13.google.en outperforms wmt13.bergamot.en.
- wmt13.microsoft.en outperforms wmt13.google.en.

#### [wmt10.es-en](es-en/wmt10.es-en.cometcompare)
- wmt10.microsoft.en outperforms wmt10.bergamot.en.
- wmt10.google.en outperforms wmt10.bergamot.en.
- wmt10.microsoft.en outperforms wmt10.google.en.

#### [wmt11.es-en](es-en/wmt11.es-en.cometcompare)
- wmt11.microsoft.en outperforms wmt11.bergamot.en.
- wmt11.google.en outperforms wmt11.bergamot.en.
- wmt11.microsoft.en outperforms wmt11.google.en.

#### [flores-dev.es-en](es-en/flores-dev.es-en.cometcompare)
- flores-dev.microsoft.en outperforms flores-dev.bergamot.en.
- flores-dev.google.en outperforms flores-dev.bergamot.en.
- flores-dev.google.en outperforms flores-dev.microsoft.en.

#### [flores-test.es-en](es-en/flores-test.es-en.cometcompare)
- flores-test.microsoft.en outperforms flores-test.bergamot.en.
- flores-test.google.en outperforms flores-test.bergamot.en.
- flores-test.google.en outperforms flores-test.microsoft.en.

#### [wmt08.es-en](es-en/wmt08.es-en.cometcompare)
- wmt08.microsoft.en outperforms wmt08.bergamot.en.
- wmt08.google.en outperforms wmt08.bergamot.en.
- wmt08.microsoft.en outperforms wmt08.google.en.

#### [mtedx_test.es-en](es-en/mtedx_test.es-en.cometcompare)
- mtedx_test.microsoft.en outperforms mtedx_test.bergamot.en.
- mtedx_test.google.en outperforms mtedx_test.bergamot.en.

#### [wmt12.es-en](es-en/wmt12.es-en.cometcompare)
- wmt12.microsoft.en outperforms wmt12.bergamot.en.
- wmt12.google.en outperforms wmt12.bergamot.en.
- wmt12.microsoft.en outperforms wmt12.google.en.

#### [wmt09.es-en](es-en/wmt09.es-en.cometcompare)
- wmt09.microsoft.en outperforms wmt09.bergamot.en.
- wmt09.google.en outperforms wmt09.bergamot.en.
- wmt09.microsoft.en outperforms wmt09.google.en.

---

## en-it

| Translator/Dataset | wmt09 | flores-test | flores-dev |
| --- | --- | --- | --- |
| bergamot | 0.64 | 0.68 | 0.70 |
| google | 0.72 (+0.07, +11.31%) | 0.78 (+0.10, +14.43%) | 0.78 (+0.08, +11.28%) |
| microsoft | 0.73 (+0.09, +13.86%) | 0.78 (+0.10, +14.07%) | 0.78 (+0.08, +10.79%) |

![Results](img/en-it-comet.png)
### Comparisons between systems
*If a comparison is omitted, the systems have equal averages (tie). Click on the dataset for a complete report*
#### [wmt09.en-it](en-it/wmt09.en-it.cometcompare)
- wmt09.microsoft.it outperforms wmt09.bergamot.it.
- wmt09.google.it outperforms wmt09.bergamot.it.
- wmt09.microsoft.it outperforms wmt09.google.it.

#### [flores-test.en-it](en-it/flores-test.en-it.cometcompare)
- flores-test.microsoft.it outperforms flores-test.bergamot.it.
- flores-test.google.it outperforms flores-test.bergamot.it.

#### [flores-dev.en-it](en-it/flores-dev.en-it.cometcompare)
- flores-dev.microsoft.it outperforms flores-dev.bergamot.it.
- flores-dev.google.it outperforms flores-dev.bergamot.it.

---

## en-pl

| Translator/Dataset | wmt20 | flores-test | flores-dev |
| --- | --- | --- | --- |
| bergamot | 0.62 | 0.67 | 0.68 |
| google | 0.78 (+0.16, +25.87%) | 0.84 (+0.17, +25.53%) | 0.85 (+0.17, +25.18%) |
| microsoft | 0.77 (+0.15, +23.45%) | 0.81 (+0.14, +21.62%) | 0.81 (+0.13, +19.77%) |

![Results](img/en-pl-comet.png)
### Comparisons between systems
*If a comparison is omitted, the systems have equal averages (tie). Click on the dataset for a complete report*
#### [wmt20.en-pl](en-pl/wmt20.en-pl.cometcompare)
- wmt20.microsoft.pl outperforms wmt20.bergamot.pl.
- wmt20.google.pl outperforms wmt20.bergamot.pl.
- wmt20.google.pl outperforms wmt20.microsoft.pl.

#### [flores-test.en-pl](en-pl/flores-test.en-pl.cometcompare)
- flores-test.microsoft.pl outperforms flores-test.bergamot.pl.
- flores-test.google.pl outperforms flores-test.bergamot.pl.
- flores-test.google.pl outperforms flores-test.microsoft.pl.

#### [flores-dev.en-pl](en-pl/flores-dev.en-pl.cometcompare)
- flores-dev.microsoft.pl outperforms flores-dev.bergamot.pl.
- flores-dev.google.pl outperforms flores-dev.bergamot.pl.
- flores-dev.google.pl outperforms flores-dev.microsoft.pl.

---

## en-es

| Translator/Dataset | flores-test | wmt12 | flores-dev | wmt13 | wmt10 | wmt11 | wmt09 | wmt08 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| bergamot | 0.64 | 0.63 | 0.64 | 0.64 | 0.64 | 0.58 | 0.58 | 0.51 |
| google | 0.76 (+0.12, +19.02%) | 0.69 (+0.06, +10.04%) | 0.75 (+0.11, +17.02%) | 0.71 (+0.06, +9.98%) | 0.72 (+0.08, +13.00%) | 0.66 (+0.08, +13.74%) | 0.65 (+0.07, +11.55%) | 0.60 (+0.10, +18.96%) |
| microsoft | 0.74 (+0.10, +16.21%) | 0.71 (+0.08, +13.38%) | 0.74 (+0.09, +14.75%) | 0.72 (+0.08, +12.08%) | 0.73 (+0.09, +13.86%) | 0.68 (+0.10, +16.92%) | 0.66 (+0.08, +13.63%) | 0.60 (+0.10, +19.53%) |

![Results](img/en-es-comet.png)
### Comparisons between systems
*If a comparison is omitted, the systems have equal averages (tie). Click on the dataset for a complete report*
#### [flores-test.en-es](en-es/flores-test.en-es.cometcompare)
- flores-test.microsoft.es outperforms flores-test.bergamot.es.
- flores-test.google.es outperforms flores-test.bergamot.es.
- flores-test.google.es outperforms flores-test.microsoft.es.

#### [wmt12.en-es](en-es/wmt12.en-es.cometcompare)
- wmt12.microsoft.es outperforms wmt12.bergamot.es.
- wmt12.google.es outperforms wmt12.bergamot.es.
- wmt12.microsoft.es outperforms wmt12.google.es.

#### [flores-dev.en-es](en-es/flores-dev.en-es.cometcompare)
- flores-dev.microsoft.es outperforms flores-dev.bergamot.es.
- flores-dev.google.es outperforms flores-dev.bergamot.es.
- flores-dev.google.es outperforms flores-dev.microsoft.es.

#### [wmt13.en-es](en-es/wmt13.en-es.cometcompare)
- wmt13.microsoft.es outperforms wmt13.bergamot.es.
- wmt13.google.es outperforms wmt13.bergamot.es.
- wmt13.microsoft.es outperforms wmt13.google.es.

#### [wmt10.en-es](en-es/wmt10.en-es.cometcompare)
- wmt10.microsoft.es outperforms wmt10.bergamot.es.
- wmt10.google.es outperforms wmt10.bergamot.es.

#### [wmt11.en-es](en-es/wmt11.en-es.cometcompare)
- wmt11.microsoft.es outperforms wmt11.bergamot.es.
- wmt11.google.es outperforms wmt11.bergamot.es.
- wmt11.microsoft.es outperforms wmt11.google.es.

#### [wmt09.en-es](en-es/wmt09.en-es.cometcompare)
- wmt09.microsoft.es outperforms wmt09.bergamot.es.
- wmt09.google.es outperforms wmt09.bergamot.es.
- wmt09.microsoft.es outperforms wmt09.google.es.

#### [wmt08.en-es](en-es/wmt08.en-es.cometcompare)
- wmt08.microsoft.es outperforms wmt08.bergamot.es.
- wmt08.google.es outperforms wmt08.bergamot.es.

---

## pl-en

| Translator/Dataset | flores-dev | wmt20 | flores-test |
| --- | --- | --- | --- |
| bergamot | 0.59 | 0.53 | 0.57 |
| google | 0.68 (+0.09, +15.30%) | 0.62 (+0.09, +17.51%) | 0.68 (+0.10, +17.70%) |
| microsoft | 0.67 (+0.08, +13.89%) | 0.64 (+0.11, +20.84%) | 0.68 (+0.10, +17.70%) |

![Results](img/pl-en-comet.png)
### Comparisons between systems
*If a comparison is omitted, the systems have equal averages (tie). Click on the dataset for a complete report*
#### [flores-dev.pl-en](pl-en/flores-dev.pl-en.cometcompare)
- flores-dev.microsoft.en outperforms flores-dev.bergamot.en.
- flores-dev.google.en outperforms flores-dev.bergamot.en.
- flores-dev.google.en outperforms flores-dev.microsoft.en.

#### [wmt20.pl-en](pl-en/wmt20.pl-en.cometcompare)
- wmt20.microsoft.en outperforms wmt20.bergamot.en.
- wmt20.google.en outperforms wmt20.bergamot.en.
- wmt20.microsoft.en outperforms wmt20.google.en.

#### [flores-test.pl-en](pl-en/flores-test.pl-en.cometcompare)
- flores-test.microsoft.en outperforms flores-test.bergamot.en.
- flores-test.google.en outperforms flores-test.bergamot.en.

---

## en-fr

| Translator/Dataset | wmt10 | flores-dev | iwslt17 | flores-test | wmt14 | wmt09 | wmt11 | wmt08 | wmt13 | wmt15 | wmt12 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| bergamot | 0.52 | 0.73 | 0.59 | 0.71 | 0.63 | 0.48 | 0.52 | 0.40 | 0.55 | 0.50 | 0.49 |
| google | 0.63 (+0.12, +22.59%) | 0.83 (+0.10, +13.28%) | 0.67 (+0.08, +13.94%) | 0.84 (+0.13, +17.81%) | 0.75 (+0.12, +19.13%) | 0.59 (+0.11, +21.82%) | 0.62 (+0.10, +18.30%) | 0.54 (+0.13, +33.43%) | 0.64 (+0.10, +17.68%) | 0.67 (+0.17, +34.26%) | 0.58 (+0.09, +18.36%) |
| microsoft | 0.65 (+0.14, +26.13%) | 0.85 (+0.11, +15.24%) | 0.69 (+0.10, +16.63%) | 0.85 (+0.14, +18.99%) | 0.78 (+0.15, +23.35%) | 0.61 (+0.13, +26.38%) | 0.64 (+0.12, +22.03%) | 0.54 (+0.14, +35.05%) | 0.66 (+0.12, +21.10%) | 0.68 (+0.18, +35.82%) | 0.61 (+0.12, +24.12%) |

![Results](img/en-fr-comet.png)
### Comparisons between systems
*If a comparison is omitted, the systems have equal averages (tie). Click on the dataset for a complete report*
#### [wmt10.en-fr](en-fr/wmt10.en-fr.cometcompare)
- wmt10.microsoft.fr outperforms wmt10.bergamot.fr.
- wmt10.google.fr outperforms wmt10.bergamot.fr.
- wmt10.microsoft.fr outperforms wmt10.google.fr.

#### [flores-dev.en-fr](en-fr/flores-dev.en-fr.cometcompare)
- flores-dev.microsoft.fr outperforms flores-dev.bergamot.fr.
- flores-dev.google.fr outperforms flores-dev.bergamot.fr.
- flores-dev.microsoft.fr outperforms flores-dev.google.fr.

#### [iwslt17.en-fr](en-fr/iwslt17.en-fr.cometcompare)
- iwslt17.microsoft.fr outperforms iwslt17.bergamot.fr.
- iwslt17.google.fr outperforms iwslt17.bergamot.fr.
- iwslt17.microsoft.fr outperforms iwslt17.google.fr.

#### [flores-test.en-fr](en-fr/flores-test.en-fr.cometcompare)
- flores-test.microsoft.fr outperforms flores-test.bergamot.fr.
- flores-test.google.fr outperforms flores-test.bergamot.fr.

#### [wmt14.en-fr](en-fr/wmt14.en-fr.cometcompare)
- wmt14.microsoft.fr outperforms wmt14.bergamot.fr.
- wmt14.google.fr outperforms wmt14.bergamot.fr.
- wmt14.microsoft.fr outperforms wmt14.google.fr.

#### [wmt09.en-fr](en-fr/wmt09.en-fr.cometcompare)
- wmt09.microsoft.fr outperforms wmt09.bergamot.fr.
- wmt09.google.fr outperforms wmt09.bergamot.fr.
- wmt09.microsoft.fr outperforms wmt09.google.fr.

#### [wmt11.en-fr](en-fr/wmt11.en-fr.cometcompare)
- wmt11.microsoft.fr outperforms wmt11.bergamot.fr.
- wmt11.google.fr outperforms wmt11.bergamot.fr.
- wmt11.microsoft.fr outperforms wmt11.google.fr.

#### [wmt08.en-fr](en-fr/wmt08.en-fr.cometcompare)
- wmt08.microsoft.fr outperforms wmt08.bergamot.fr.
- wmt08.google.fr outperforms wmt08.bergamot.fr.

#### [wmt13.en-fr](en-fr/wmt13.en-fr.cometcompare)
- wmt13.microsoft.fr outperforms wmt13.bergamot.fr.
- wmt13.google.fr outperforms wmt13.bergamot.fr.
- wmt13.microsoft.fr outperforms wmt13.google.fr.

#### [wmt15.en-fr](en-fr/wmt15.en-fr.cometcompare)
- wmt15.microsoft.fr outperforms wmt15.bergamot.fr.
- wmt15.google.fr outperforms wmt15.bergamot.fr.

#### [wmt12.en-fr](en-fr/wmt12.en-fr.cometcompare)
- wmt12.microsoft.fr outperforms wmt12.bergamot.fr.
- wmt12.google.fr outperforms wmt12.bergamot.fr.
- wmt12.microsoft.fr outperforms wmt12.google.fr.

---

## et-en

| Translator/Dataset | flores-dev | flores-test | wmt18 |
| --- | --- | --- | --- |
| bergamot | 0.63 | 0.64 | 0.52 |
| google | 0.81 (+0.18, +27.76%) | 0.79 (+0.15, +24.06%) | 0.70 (+0.18, +33.71%) |
| microsoft | 0.78 (+0.15, +22.94%) | 0.76 (+0.12, +19.44%) | 0.67 (+0.15, +29.00%) |

![Results](img/et-en-comet.png)
### Comparisons between systems
*If a comparison is omitted, the systems have equal averages (tie). Click on the dataset for a complete report*
#### [flores-dev.et-en](et-en/flores-dev.et-en.cometcompare)
- flores-dev.microsoft.en outperforms flores-dev.bergamot.en.
- flores-dev.google.en outperforms flores-dev.bergamot.en.
- flores-dev.google.en outperforms flores-dev.microsoft.en.

#### [flores-test.et-en](et-en/flores-test.et-en.cometcompare)
- flores-test.microsoft.en outperforms flores-test.bergamot.en.
- flores-test.google.en outperforms flores-test.bergamot.en.
- flores-test.google.en outperforms flores-test.microsoft.en.

#### [wmt18.et-en](et-en/wmt18.et-en.cometcompare)
- wmt18.microsoft.en outperforms wmt18.bergamot.en.
- wmt18.google.en outperforms wmt18.bergamot.en.
- wmt18.google.en outperforms wmt18.microsoft.en.

---

## bg-en

| Translator/Dataset | flores-dev | flores-test |
| --- | --- | --- |
| bergamot | 0.68 | 0.68 |
| google | 0.75 (+0.07, +10.71%) | 0.75 (+0.07, +10.26%) |
| microsoft | 0.73 (+0.05, +7.18%) | 0.73 (+0.05, +6.92%) |

![Results](img/bg-en-comet.png)
### Comparisons between systems
*If a comparison is omitted, the systems have equal averages (tie). Click on the dataset for a complete report*
#### [flores-dev.bg-en](bg-en/flores-dev.bg-en.cometcompare)
- flores-dev.microsoft.en outperforms flores-dev.bergamot.en.
- flores-dev.google.en outperforms flores-dev.bergamot.en.
- flores-dev.google.en outperforms flores-dev.microsoft.en.

#### [flores-test.bg-en](bg-en/flores-test.bg-en.cometcompare)
- flores-test.microsoft.en outperforms flores-test.bergamot.en.
- flores-test.google.en outperforms flores-test.bergamot.en.
- flores-test.google.en outperforms flores-test.microsoft.en.

---

## de-en

| Translator/Dataset | wmt16 | wmt13 | iwslt17 | wmt10 | wmt17 | wmt21 | wmt14 | wmt19 | wmt11 | flores-dev | wmt22 | wmt20 | flores-test | wmt15 | wmt08 | wmt12 | wmt09 | wmt18 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| bergamot | 0.56 | 0.51 | 0.48 | 0.45 | 0.52 | 0.48 | 0.49 | 0.41 | 0.39 | 0.68 | 0.40 | 0.54 | 0.68 | 0.52 | 0.39 | 0.39 | 0.41 | 0.58 |
| google | 0.67 (+0.11, +19.50%) | 0.59 (+0.09, +16.79%) | 0.57 (+0.09, +18.39%) | 0.57 (+0.12, +26.27%) | 0.65 (+0.13, +25.09%) | 0.61 (+0.13, +27.30%) | 0.62 (+0.13, +27.07%) | 0.56 (+0.14, +34.37%) | 0.48 (+0.09, +24.10%) | 0.76 (+0.08, +11.51%) | 0.56 (+0.16, +40.53%) | 0.66 (+0.12, +22.01%) | 0.76 (+0.08, +11.57%) | 0.64 (+0.12, +22.71%) | 0.51 (+0.12, +29.36%) | 0.52 (+0.13, +32.18%) | 0.51 (+0.10, +25.46%) | 0.70 (+0.11, +19.06%) |
| microsoft | 0.69 (+0.13, +22.98%) | 0.62 (+0.11, +21.80%) | 0.58 (+0.10, +20.87%) | 0.59 (+0.14, +31.46%) | 0.66 (+0.14, +27.41%) | 0.62 (+0.14, +30.21%) | 0.63 (+0.14, +29.25%) | 0.59 (+0.17, +41.07%) | 0.53 (+0.14, +34.74%) | 0.77 (+0.09, +13.67%) | 0.55 (+0.15, +38.95%) | 0.69 (+0.15, +27.97%) | 0.77 (+0.09, +13.19%) | 0.65 (+0.13, +24.73%) | 0.53 (+0.13, +34.22%) | 0.55 (+0.16, +39.48%) | 0.54 (+0.13, +31.15%) | 0.72 (+0.13, +23.05%) |

![Results](img/de-en-comet.png)
### Comparisons between systems
*If a comparison is omitted, the systems have equal averages (tie). Click on the dataset for a complete report*
#### [wmt16.de-en](de-en/wmt16.de-en.cometcompare)
- wmt16.microsoft.en outperforms wmt16.bergamot.en.
- wmt16.google.en outperforms wmt16.bergamot.en.
- wmt16.microsoft.en outperforms wmt16.google.en.

#### [wmt13.de-en](de-en/wmt13.de-en.cometcompare)
- wmt13.microsoft.en outperforms wmt13.bergamot.en.
- wmt13.google.en outperforms wmt13.bergamot.en.
- wmt13.microsoft.en outperforms wmt13.google.en.

#### [iwslt17.de-en](de-en/iwslt17.de-en.cometcompare)
- iwslt17.microsoft.en outperforms iwslt17.bergamot.en.
- iwslt17.google.en outperforms iwslt17.bergamot.en.
- iwslt17.microsoft.en outperforms iwslt17.google.en.

#### [wmt10.de-en](de-en/wmt10.de-en.cometcompare)
- wmt10.microsoft.en outperforms wmt10.bergamot.en.
- wmt10.google.en outperforms wmt10.bergamot.en.
- wmt10.microsoft.en outperforms wmt10.google.en.

#### [wmt17.de-en](de-en/wmt17.de-en.cometcompare)
- wmt17.microsoft.en outperforms wmt17.bergamot.en.
- wmt17.google.en outperforms wmt17.bergamot.en.
- wmt17.microsoft.en outperforms wmt17.google.en.

#### [wmt21.de-en](de-en/wmt21.de-en.cometcompare)
- wmt21.microsoft.en outperforms wmt21.bergamot.en.
- wmt21.google.en outperforms wmt21.bergamot.en.
- wmt21.microsoft.en outperforms wmt21.google.en.

#### [wmt14.de-en](de-en/wmt14.de-en.cometcompare)
- wmt14.microsoft.en outperforms wmt14.bergamot.en.
- wmt14.google.en outperforms wmt14.bergamot.en.
- wmt14.microsoft.en outperforms wmt14.google.en.

#### [wmt19.de-en](de-en/wmt19.de-en.cometcompare)
- wmt19.microsoft.en outperforms wmt19.bergamot.en.
- wmt19.google.en outperforms wmt19.bergamot.en.
- wmt19.microsoft.en outperforms wmt19.google.en.

#### [wmt11.de-en](de-en/wmt11.de-en.cometcompare)
- wmt11.microsoft.en outperforms wmt11.bergamot.en.
- wmt11.google.en outperforms wmt11.bergamot.en.
- wmt11.microsoft.en outperforms wmt11.google.en.

#### [flores-dev.de-en](de-en/flores-dev.de-en.cometcompare)
- flores-dev.microsoft.en outperforms flores-dev.bergamot.en.
- flores-dev.google.en outperforms flores-dev.bergamot.en.
- flores-dev.microsoft.en outperforms flores-dev.google.en.

#### [wmt22.de-en](de-en/wmt22.de-en.cometcompare)
- wmt22.microsoft.en outperforms wmt22.bergamot.en.
- wmt22.google.en outperforms wmt22.bergamot.en.

#### [wmt20.de-en](de-en/wmt20.de-en.cometcompare)
- wmt20.microsoft.en outperforms wmt20.bergamot.en.
- wmt20.google.en outperforms wmt20.bergamot.en.
- wmt20.microsoft.en outperforms wmt20.google.en.

#### [flores-test.de-en](de-en/flores-test.de-en.cometcompare)
- flores-test.microsoft.en outperforms flores-test.bergamot.en.
- flores-test.google.en outperforms flores-test.bergamot.en.
- flores-test.microsoft.en outperforms flores-test.google.en.

#### [wmt15.de-en](de-en/wmt15.de-en.cometcompare)
- wmt15.microsoft.en outperforms wmt15.bergamot.en.
- wmt15.google.en outperforms wmt15.bergamot.en.
- wmt15.microsoft.en outperforms wmt15.google.en.

#### [wmt08.de-en](de-en/wmt08.de-en.cometcompare)
- wmt08.microsoft.en outperforms wmt08.bergamot.en.
- wmt08.google.en outperforms wmt08.bergamot.en.
- wmt08.microsoft.en outperforms wmt08.google.en.

#### [wmt12.de-en](de-en/wmt12.de-en.cometcompare)
- wmt12.microsoft.en outperforms wmt12.bergamot.en.
- wmt12.google.en outperforms wmt12.bergamot.en.
- wmt12.microsoft.en outperforms wmt12.google.en.

#### [wmt09.de-en](de-en/wmt09.de-en.cometcompare)
- wmt09.microsoft.en outperforms wmt09.bergamot.en.
- wmt09.google.en outperforms wmt09.bergamot.en.
- wmt09.microsoft.en outperforms wmt09.google.en.

#### [wmt18.de-en](de-en/wmt18.de-en.cometcompare)
- wmt18.microsoft.en outperforms wmt18.bergamot.en.
- wmt18.google.en outperforms wmt18.bergamot.en.
- wmt18.microsoft.en outperforms wmt18.google.en.

---

## en-cs

| Translator/Dataset | wmt13 | wmt08 | wmt20 | wmt18 | wmt12 | flores-test | wmt22 | wmt15 | wmt19 | flores-dev | wmt10 | wmt21 | wmt11 | wmt17 | wmt16 | wmt14 | wmt09 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| bergamot | 0.68 | 0.54 | 0.55 | 0.63 | 0.55 | 0.70 | 0.62 | 0.66 | 0.52 | 0.68 | 0.61 | 0.46 | 0.56 | 0.62 | 0.64 | 0.75 | 0.60 |
| google | 0.85 (+0.17, +24.72%) | 0.78 (+0.23, +43.36%) | 0.78 (+0.23, +41.54%) | 0.81 (+0.18, +29.20%) | 0.76 (+0.21, +37.61%) | 0.94 (+0.23, +33.13%) | 0.97 (+0.36, +57.96%) | 0.86 (+0.20, +29.98%) | 0.72 (+0.20, +38.74%) | 0.93 (+0.25, +36.44%) | 0.81 (+0.20, +33.54%) | 0.65 (+0.19, +40.85%) | 0.77 (+0.21, +37.08%) | 0.81 (+0.19, +30.14%) | 0.85 (+0.21, +32.72%) | 0.95 (+0.20, +26.46%) | 0.81 (+0.22, +36.87%) |
| microsoft | 0.87 (+0.19, +27.50%) | 0.78 (+0.24, +44.75%) | 0.81 (+0.26, +47.71%) | 0.82 (+0.20, +31.49%) | 0.78 (+0.23, +41.83%) | 0.93 (+0.23, +32.76%) | 0.94 (+0.32, +52.78%) | 0.87 (+0.21, +31.11%) | 0.77 (+0.25, +49.14%) | 0.93 (+0.25, +36.25%) | 0.83 (+0.22, +35.78%) | 0.69 (+0.23, +49.02%) | 0.80 (+0.24, +41.92%) | 0.83 (+0.20, +32.21%) | 0.85 (+0.21, +33.51%) | 0.97 (+0.22, +29.34%) | 0.82 (+0.22, +37.76%) |

![Results](img/en-cs-comet.png)
### Comparisons between systems
*If a comparison is omitted, the systems have equal averages (tie). Click on the dataset for a complete report*
#### [wmt13.en-cs](en-cs/wmt13.en-cs.cometcompare)
- wmt13.microsoft.cs outperforms wmt13.bergamot.cs.
- wmt13.google.cs outperforms wmt13.bergamot.cs.
- wmt13.microsoft.cs outperforms wmt13.google.cs.

#### [wmt08.en-cs](en-cs/wmt08.en-cs.cometcompare)
- wmt08.microsoft.cs outperforms wmt08.bergamot.cs.
- wmt08.google.cs outperforms wmt08.bergamot.cs.

#### [wmt20.en-cs](en-cs/wmt20.en-cs.cometcompare)
- wmt20.microsoft.cs outperforms wmt20.bergamot.cs.
- wmt20.google.cs outperforms wmt20.bergamot.cs.
- wmt20.microsoft.cs outperforms wmt20.google.cs.

#### [wmt18.en-cs](en-cs/wmt18.en-cs.cometcompare)
- wmt18.microsoft.cs outperforms wmt18.bergamot.cs.
- wmt18.google.cs outperforms wmt18.bergamot.cs.
- wmt18.microsoft.cs outperforms wmt18.google.cs.

#### [wmt12.en-cs](en-cs/wmt12.en-cs.cometcompare)
- wmt12.microsoft.cs outperforms wmt12.bergamot.cs.
- wmt12.google.cs outperforms wmt12.bergamot.cs.
- wmt12.microsoft.cs outperforms wmt12.google.cs.

#### [flores-test.en-cs](en-cs/flores-test.en-cs.cometcompare)
- flores-test.microsoft.cs outperforms flores-test.bergamot.cs.
- flores-test.google.cs outperforms flores-test.bergamot.cs.

#### [wmt22.en-cs](en-cs/wmt22.en-cs.cometcompare)
- wmt22.microsoft.cs outperforms wmt22.bergamot.cs.
- wmt22.google.cs outperforms wmt22.bergamot.cs.
- wmt22.google.cs outperforms wmt22.microsoft.cs.

#### [wmt15.en-cs](en-cs/wmt15.en-cs.cometcompare)
- wmt15.microsoft.cs outperforms wmt15.bergamot.cs.
- wmt15.google.cs outperforms wmt15.bergamot.cs.

#### [wmt19.en-cs](en-cs/wmt19.en-cs.cometcompare)
- wmt19.microsoft.cs outperforms wmt19.bergamot.cs.
- wmt19.google.cs outperforms wmt19.bergamot.cs.
- wmt19.microsoft.cs outperforms wmt19.google.cs.

#### [flores-dev.en-cs](en-cs/flores-dev.en-cs.cometcompare)
- flores-dev.microsoft.cs outperforms flores-dev.bergamot.cs.
- flores-dev.google.cs outperforms flores-dev.bergamot.cs.

#### [wmt10.en-cs](en-cs/wmt10.en-cs.cometcompare)
- wmt10.microsoft.cs outperforms wmt10.bergamot.cs.
- wmt10.google.cs outperforms wmt10.bergamot.cs.
- wmt10.microsoft.cs outperforms wmt10.google.cs.

#### [wmt21.en-cs](en-cs/wmt21.en-cs.cometcompare)
- wmt21.microsoft.cs outperforms wmt21.bergamot.cs.
- wmt21.google.cs outperforms wmt21.bergamot.cs.
- wmt21.microsoft.cs outperforms wmt21.google.cs.

#### [wmt11.en-cs](en-cs/wmt11.en-cs.cometcompare)
- wmt11.microsoft.cs outperforms wmt11.bergamot.cs.
- wmt11.google.cs outperforms wmt11.bergamot.cs.
- wmt11.microsoft.cs outperforms wmt11.google.cs.

#### [wmt17.en-cs](en-cs/wmt17.en-cs.cometcompare)
- wmt17.microsoft.cs outperforms wmt17.bergamot.cs.
- wmt17.google.cs outperforms wmt17.bergamot.cs.
- wmt17.microsoft.cs outperforms wmt17.google.cs.

#### [wmt16.en-cs](en-cs/wmt16.en-cs.cometcompare)
- wmt16.microsoft.cs outperforms wmt16.bergamot.cs.
- wmt16.google.cs outperforms wmt16.bergamot.cs.

#### [wmt14.en-cs](en-cs/wmt14.en-cs.cometcompare)
- wmt14.microsoft.cs outperforms wmt14.bergamot.cs.
- wmt14.google.cs outperforms wmt14.bergamot.cs.
- wmt14.microsoft.cs outperforms wmt14.google.cs.

#### [wmt09.en-cs](en-cs/wmt09.en-cs.cometcompare)
- wmt09.microsoft.cs outperforms wmt09.bergamot.cs.
- wmt09.google.cs outperforms wmt09.bergamot.cs.

---

## cs-en

| Translator/Dataset | wmt16 | wmt13 | wmt10 | wmt17 | wmt21 | wmt14 | wmt11 | flores-dev | wmt22 | wmt20 | flores-test | wmt15 | wmt08 | wmt12 | wmt09 | wmt18 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| bergamot | 0.48 | 0.50 | 0.44 | 0.45 | 0.47 | 0.57 | 0.41 | 0.65 | 0.55 | 0.35 | 0.65 | 0.49 | 0.37 | 0.42 | 0.43 | 0.48 |
| google | 0.62 (+0.14, +28.50%) | 0.61 (+0.12, +23.25%) | 0.57 (+0.13, +29.95%) | 0.58 (+0.13, +28.12%) | 0.60 (+0.13, +27.51%) | 0.70 (+0.13, +22.40%) | 0.53 (+0.12, +29.26%) | 0.76 (+0.10, +15.71%) | 0.70 (+0.15, +27.55%) | 0.51 (+0.16, +46.19%) | 0.77 (+0.11, +17.45%) | 0.62 (+0.13, +26.40%) | 0.52 (+0.15, +41.56%) | 0.54 (+0.12, +28.77%) | 0.56 (+0.13, +30.83%) | 0.59 (+0.11, +23.27%) |
| microsoft | 0.62 (+0.14, +28.46%) | 0.63 (+0.14, +27.56%) | 0.58 (+0.14, +30.79%) | 0.57 (+0.13, +28.01%) | 0.59 (+0.12, +24.74%) | 0.72 (+0.14, +24.79%) | 0.56 (+0.15, +35.20%) | 0.75 (+0.10, +14.95%) | 0.72 (+0.17, +30.46%) | 0.50 (+0.16, +44.44%) | 0.76 (+0.11, +16.30%) | 0.63 (+0.14, +27.93%) | 0.52 (+0.15, +41.59%) | 0.56 (+0.14, +33.29%) | 0.57 (+0.14, +32.48%) | 0.60 (+0.12, +25.68%) |

![Results](img/cs-en-comet.png)
### Comparisons between systems
*If a comparison is omitted, the systems have equal averages (tie). Click on the dataset for a complete report*
#### [wmt16.cs-en](cs-en/wmt16.cs-en.cometcompare)
- wmt16.microsoft.en outperforms wmt16.bergamot.en.
- wmt16.google.en outperforms wmt16.bergamot.en.

#### [wmt13.cs-en](cs-en/wmt13.cs-en.cometcompare)
- wmt13.microsoft.en outperforms wmt13.bergamot.en.
- wmt13.google.en outperforms wmt13.bergamot.en.
- wmt13.microsoft.en outperforms wmt13.google.en.

#### [wmt10.cs-en](cs-en/wmt10.cs-en.cometcompare)
- wmt10.microsoft.en outperforms wmt10.bergamot.en.
- wmt10.google.en outperforms wmt10.bergamot.en.

#### [wmt17.cs-en](cs-en/wmt17.cs-en.cometcompare)
- wmt17.microsoft.en outperforms wmt17.bergamot.en.
- wmt17.google.en outperforms wmt17.bergamot.en.

#### [wmt21.cs-en](cs-en/wmt21.cs-en.cometcompare)
- wmt21.microsoft.en outperforms wmt21.bergamot.en.
- wmt21.google.en outperforms wmt21.bergamot.en.
- wmt21.google.en outperforms wmt21.microsoft.en.

#### [wmt14.cs-en](cs-en/wmt14.cs-en.cometcompare)
- wmt14.microsoft.en outperforms wmt14.bergamot.en.
- wmt14.google.en outperforms wmt14.bergamot.en.
- wmt14.microsoft.en outperforms wmt14.google.en.

#### [wmt11.cs-en](cs-en/wmt11.cs-en.cometcompare)
- wmt11.microsoft.en outperforms wmt11.bergamot.en.
- wmt11.google.en outperforms wmt11.bergamot.en.
- wmt11.microsoft.en outperforms wmt11.google.en.

#### [flores-dev.cs-en](cs-en/flores-dev.cs-en.cometcompare)
- flores-dev.microsoft.en outperforms flores-dev.bergamot.en.
- flores-dev.google.en outperforms flores-dev.bergamot.en.

#### [wmt22.cs-en](cs-en/wmt22.cs-en.cometcompare)
- wmt22.microsoft.en outperforms wmt22.bergamot.en.
- wmt22.google.en outperforms wmt22.bergamot.en.
- wmt22.microsoft.en outperforms wmt22.google.en.

#### [wmt20.cs-en](cs-en/wmt20.cs-en.cometcompare)
- wmt20.microsoft.en outperforms wmt20.bergamot.en.
- wmt20.google.en outperforms wmt20.bergamot.en.

#### [flores-test.cs-en](cs-en/flores-test.cs-en.cometcompare)
- flores-test.microsoft.en outperforms flores-test.bergamot.en.
- flores-test.google.en outperforms flores-test.bergamot.en.
- flores-test.google.en outperforms flores-test.microsoft.en.

#### [wmt15.cs-en](cs-en/wmt15.cs-en.cometcompare)
- wmt15.microsoft.en outperforms wmt15.bergamot.en.
- wmt15.google.en outperforms wmt15.bergamot.en.

#### [wmt08.cs-en](cs-en/wmt08.cs-en.cometcompare)
- wmt08.microsoft.en outperforms wmt08.bergamot.en.
- wmt08.google.en outperforms wmt08.bergamot.en.

#### [wmt12.cs-en](cs-en/wmt12.cs-en.cometcompare)
- wmt12.microsoft.en outperforms wmt12.bergamot.en.
- wmt12.google.en outperforms wmt12.bergamot.en.
- wmt12.microsoft.en outperforms wmt12.google.en.

#### [wmt09.cs-en](cs-en/wmt09.cs-en.cometcompare)
- wmt09.microsoft.en outperforms wmt09.bergamot.en.
- wmt09.google.en outperforms wmt09.bergamot.en.
- wmt09.microsoft.en outperforms wmt09.google.en.

#### [wmt18.cs-en](cs-en/wmt18.cs-en.cometcompare)
- wmt18.microsoft.en outperforms wmt18.bergamot.en.
- wmt18.google.en outperforms wmt18.bergamot.en.
- wmt18.microsoft.en outperforms wmt18.google.en.

---