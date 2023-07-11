## Evaluation of spacy 2.2.4 models by Stefan

There are 7 trained models. 6 of which have evaluation data in their folder.

This evaluation data exists in these formats:
- txt (1x: 2019-12-03)
- pickle (4x: 2020-01-02 - 2020-04-16)
- json (1x: 2020-04-30)

For the `txt` and `pickle` files there are parsing functions scattered around this repo. Importing
them from their modules however causes execution of the modules which leads to crashes as a lot of
context is missing. In order to avoid changes to an undocumented and sprawled codebase, but still
to reuse code and its context, relevant code was copied / imported here. For the `json` file, no
existing parsing function was found, so one was implemented.

There were also existing evaluation functions compatible with the pickle files of the models
2020-01-02 - 2020-04-16, so that was copied here and reused. For the others, custom evaluation
logic was implemented, using spaCy's function on the `txt` and a custom one on the `json` file as
that data was a in shape incompatible with spaCy's function.

The commit of the remaining code base which was copied or imported from is https://gitlab.oeaw.ac.at/acdh-ch/apis/spacy-ner/-/tree/8e75d3561e617f1bd135d4c06fbb982285f6f544

## Evaluation summary

- model: **ner_apis_2019-12-03_23:32:24**
  - evaluation data description:
    - evaluation file: ner_apis_2019-12-03_23:32:24/corpus/evalset.txt
    - evaluation data size: count sentences: 3042, count NER tags: 1657
    - NER tags: ('LOC', 'MISC', 'ORG', 'PER')
  - evaluations:
    - spacy's evaluation: **p: 53.85, r: 51.29**
- model: **ner_apis_2020-01-02_12:34:48**
  - evaluation data description:
    - evaluation file: ner_apis_2020-01-02_12:34:48/corpus/evalset.pickle
    - evaluation data size: count sentences: 2474, count NER tags: 1647
    - NER tags: ('LOC', 'ORG')
  - evaluations:
    - manual evaluation: **p: 76.86, r: 38.92**
    - spacy's evaluation (E0) with 'ner' pipe: **p: 61.79, r: 47.92**
- model: **ner_apis_2020-01-29_13:19:53**
  - evaluation data description:
    - evaluation file: ner_apis_2020-01-29_13:19:53/corpus/evalset.pickle
    - evaluation data size: count sentences: 832, count NER tags: 1557
    - NER tags: ('LOC', 'MISC', 'ORG', 'PER')
  - evaluations:
    - manual evaluation: **p: 72.04, r: 74.84**
    - spacy's evaluation (E0) with 'ner' pipe: **p: 76.42, r: 71.47**
- model: **ner_apis_2020-04-07_15:00:35**
  - evaluation data description:
    - evaluation file: ner_apis_2020-04-07_15:00:35/corpus/evalset.pickle
    - evaluation data size: count sentences: 861, count NER tags: 1804
    - NER tags: ('LOC', 'MISC', 'ORG', 'PER')
  - evaluations:
    - manual evaluation: **p: 72.45, r: 82.33**
    - spacy's evaluation (E0) with 'ner' pipe: **p: 77.71, r: 81.18**
    - spacy's evaluation (E1) with 'tagger', 'parser', 'ner' pipes: **p: 75.62, r: 77.64**
- model: **ner_apis_2020-04-16_14:21:46**
  - evaluation data description:
    - evaluation file: ner_apis_2020-04-16_14:21:46/corpus/evalset.pickle
    - evaluation data size: count sentences: 866, count NER tags: 1878
    - NER tags: ('LOC', 'MISC', 'ORG', 'PER')
  - evaluations:
    - manual evaluation: **p: 53.38, r: 49.38**
    - spacy's evaluation (E0) with 'ner' pipe: **p: 54.81, r: 43.25**
    - spacy's evaluation (E1) with 'tagger', 'parser', 'ner' pipes: **p: 54.19, r: 41.84**
- model: **ner_apis_2020-04-30_11:24:09**
  - evaluation data description:
    - evaluation file: ner_apis_2020-04-30_11:24:09/corpus/evalset.json
    - evaluation data size: count sentences: 904, count NER tags: 3144
    - NER tags: ('LOC', 'MISC', 'ORG', 'PER')
  - evaluations:
    - manual evaluation: **p: 81.77, r: 23.6**

## How to reproduce

I don't know the exact versions of the python interpreter and packages that were used to build this
codebase, but I could get the model loading and this evaluation here running by using:

- python 3.6.9 (needed for the unpickling of some eval data sets, 3.8 crashed)

TODO
