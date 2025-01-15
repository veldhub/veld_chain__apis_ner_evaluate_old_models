# veld_chain__apis_ner_evaluate_old_models

This repo contains [chain velds](https://zenodo.org/records/13322913) encapsulating evalution of 
old spacy models, trained in the 
[APIS](https://www.oeaw.ac.at/acdh/research/dh-research-infrastructure/activities/modelling-humanities-data/apis) 
/ [ÖBL](https://www.oeaw.ac.at/acdh/research/dh-research-infrastructure/activities/modelling-humanities-data/oebl-austrian-biographical-dictionary) 
context.

## requirements

- git
- docker compose (note: older docker compose versions require running `docker-compose` instead of 
  `docker compose`)

Clone this repo with all its submodules
```
git clone --recurse-submodules https://github.com/veldhub/veld_chain__apis_ner_evaluate_old_models.git
```

## how to reproduce

**[./veld_evaluate.yaml](./veld_evaluate.yaml)** 

Reruns the evalation. Note: I couldn't find out the exact versions of the python interpreter and
packages that were used to train the models, but I could get the models loading and this evaluation
running by using python 3.7.6 (3.8 or higher would crash when unpickling some eval data sets) and
spacy 2.2.4 .

```
docker compose -f veld_evaluate.yaml up
```

## Evaluation results

The results are written directly into apis spacy ner repo: 
https://gitlab.oeaw.ac.at/acdh-ch/apis/spacy-ner/-/blob/master/reevaluations_all.md 

