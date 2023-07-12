## experimental veld repo

For the current work on VELD, I need real life examples to use. This repo is one. It both serves
the purpose of evaluating models previously trained so that they can be used in the intavia project
and also compared to models trained with spacy3 to check for potential improvement. 

At the same time, I encapsulate this work into an experimental setup to field-trial VELD 
prototypes.

## Evaluation of spacy 2.2.4 models by Stefan

There are 7 trained models in https://gitlab.oeaw.ac.at/acdh-ch/apis/spacy-ner .

6 of those have evaluation data in their folder, so that is used to validate the models.

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

## Evaluation results

The results are written directly into apis spacy ner repo: https://gitlab.oeaw.ac.at/acdh-ch/apis/spacy-ner/-/blob/master/reevaluations_all.md 

## How to reproduce

I don't know the exact versions of the python interpreter and packages that were used to train the
models, but I could get the models loading and this evaluation running by using python 3.6.15 (3.8 
or higher would crash when unpickling some eval data sets) and spacy 2.2.4 .

The evaluation code for all models in one go can be rerun in the VELD context by using the docker 
definition in the `veld.yaml` and the relevant submodules by:

- cloning this repo inlcuding all subrepos:
```
git clone --recurse-submodules https://gitlab.oeaw.ac.at/acdh-ch/nlp/veld_chain_5_apis_ner_evaluate_old_models.git
```

- running it as a docker compose service:
```
docker compose -f veld.yaml up
```
