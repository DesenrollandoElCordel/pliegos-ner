# Named Entity Recognition for 19th-century Spanish Chapobooks

This repository contains the datasets and the scripts we used to train our NER model with the [Flair](https://github.com/flairNLP/flair/tree/master) framework, as well as the results. This model allows to detect only the placenames in our collection of 19th-century chapbooks.

## Groundtruth
We performed several trainings by varying the number of documents in the groundtruth (GT):

- [Corpus](/trainings/corpus): 50 documents randomly selected from the two corpora of the projet (3131 sentences, 368 LOC) ;
- [Corpus extended](/trainings/corpus-extended): 10 extra texts added to the precedent corpus, randomly selected as well (4032 sentences, 425 LOC).

In both cases, to prepare the GT, we applied the Flair model *ner-spanish-large* to those documents and, then, corrected the results with [INCEpTION](https://inception-project.github.io/).

## Trainings
The script we used for the fine-tuning of the different models can be found [here](trainings/flair_fine_tuning.ipynb).
### Fine-tuning of *ner-spanish-large* (Flair's model)
The application of the default Spanish NER model of Flair allowed us to obtained a F1-Score of 92%. To improve the performance of this model, we have chosen to fine-tune it. The results are available [here](trainings/Results_test_GPU/Resultat_Ner-spanish-large.txt).

|   |F1-Score   | Precision  | Recall |
|---|---|---|---|
|50 texts, 10 epochs     | 92,68%  | 95,74%  | 90% |
|60 texts, 20 epochs     | 90,91%  | 91,67%  | 90% |

### Fine-tuning of *mlm-spanish-roberta-base* (MGG)

The fine-tuning of another model, [*mlm-spanish-roberta-base*](https://huggingface.co/MMG/mlm-spanish-roberta-base), gives a better recall than *ner-spanish-large* with 60 texts and 20 epochs. However, the fine-tuned models did not outperform it when it comes to precision, which is more important for our project than recall.
The detailled results are available [here](/trainings/Results_test_GPU/Resultat_Ner_Roberta.txt).

|   |F1-Score   | Precision  | Recall |
|---|---|---|---|
|50 texts, 10 epochs     | 88,24%  | 86,54%  | 90% |
|60 texts, 20 epochs     | 90,38%  | 87,04%  | 94% |

### Fine-tuning of *bert-spanish-cased-finetuned-ner* (Manuel Romero)
We obtained our [best model](/trainings/ner-bertSpanish-BestModel) by fine-tuning a third model, [*bert-spanish-cased-finetuned-ner*](https://huggingface.co/mrm8488/bert-spanish-cased-finetuned-ner), whose results seemed promising for our corpus.
The detailed results are available [here](/trainings).

|   |F1-Score   | Precision  | Recall |
|---|---|---|---|
|50 texts, 10 epochs     | 90%  | 87%  | 94% |
|60 texts, 10 epochs     | 95,08%  | 95,08%  | 95% |
|**60 texts, 20 epochs**     | **95,87%**  | **96,67%**  | **95,08%** |

## Results

The [results](moreno-ner/moreno-IOB), obtained with our best model, have been exported in CoNLL 2002 format, which follows the [BIO format](https://en.wikipedia.org/wiki/Inside%E2%80%93outside%E2%80%93beginning_(tagging)), with this [script](moreno-ner/ner-corpus-moreno.ipynb). To develop different visualisations with the place names, we transformed these results into several CSV files:

- Extraction of the [place names](moreno-ner/nerList_Moreno.csv), with [ner2csv.py](../code-python/ner2csv.py).
- Enrichment of the [CSV file](moreno-ner/nerList_Moreno_Wikidata.csv) with information extracted from Wikidata thanks to *Open Refine*  (Wikidata identifier, geographical coordinates, type of place, normalised names).
- Addition of [information](moreno-ner/nerList_Moreno_enriched.csv) extracted from the XML TEI files (document's title, printer, publication place, date, type of text, URL of the document) and enrichment of the TEI files with geographical data, with [ner2tei.py](../code-python/ner2tei.py).
- Conversion in JSON to create a map with an application called [Peripleo](../peripleo-pliegos) with [csv2json.py](../code-python/csv2json.py).