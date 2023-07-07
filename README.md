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
The application of the default Spanish NER model of Flair allowed us to obtained a F1-Score of 92%. To improve the performance of this model, we have chosen to fine-tune it. The results are available [here](trainings/Results_test_GPU/Resultat_Ner-spanish-large.txt):

|   |F1-Score   | Precision  | Recall |
|---|---|---|---|
|50 texts, 10 epochs     | 92,68%  | 95,74%  | 90% |
|60 texts, 20 epochs     | 90,91%  | 91,67%  | 90% |

### Fine-tuning of *roberta-spanish-ner* (MGG)

Work in progress...

## Results

Work in progress...

## The case of the catalan chapbooks

Work in progress...
