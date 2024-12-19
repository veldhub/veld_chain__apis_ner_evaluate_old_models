# APIS NER evaluate

This chain veld evalutes old spacy models, trained in the APIS / ÖBL context.

## Evaluation results

The results are written directly into apis spacy ner repo: 
https://gitlab.oeaw.ac.at/acdh-ch/apis/spacy-ner/-/blob/master/reevaluations_all.md 

## How to reproduce

I don't know the exact versions of the python interpreter and packages that were used to train the
models, but I could get the models loading and this evaluation running by using python 3.7.6 (3.8 
or higher would crash when unpickling some eval data sets) and spacy 2.2.4 .

The evaluation code for all models in one go can be rerun in the VELD context by using the docker 
definition in the `veld.yaml` and the relevant submodules by:

- cloning this repo inlcuding all subrepos (this takes a while as spacy ner has a size of 20GB):
```
git clone --recurse-submodules https://github.com/veldhub/veld_chain__apis_ner_evaluate_old_models.git
```

- running it as a docker compose service:
```
docker compose -f veld_evaluate.yaml up
```
