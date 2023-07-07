# Named Entity Recognition for 19th-century Spanish Chapobooks

This repository contains the datasets and the scripts we used to train our NER model with the [Flair](https://github.com/flairNLP/flair/tree/master) framework, as well as the results. This model allows to detect only the namespaces in our collection of 19th-century chapbooks.

## Groundtruth

We performed several trainings by varying the number of documents in the groundtruth (GT):

- [Corpus](/trainings/corpus): 50 documents randomly selected from the two corpora of the projet (3131 sentences, 368 LOC) ;
- [Corpus extended](/trainings/corpus-extended): 10 extra texts added to the precedent corpus, randomly selected as well (4032 sentences, 425 LOC).

In both cases, to prepare the GT, we applied the Flair model *ner-spanish-large* to those documents and, then, corrected the results with [Inception](https://inception-project.github.io/).

## Trainings
