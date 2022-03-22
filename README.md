# Stack Overflow (Duplicity) Dataset

This repository publishes two novel datasets for (pre-)training NLP models applicable for software engineering domain.
The datasets were presented in the paper [MQDD – Pre-training of Multimodal Question Duplicity Detection for Software Engineering Domain](https://arxiv.org/abs/xxx),
which contains detailed information about the datasets.


## Stack Overflow Dataset (SOD)

**Download the dataset:**

The SOD dataset can be obtained from our GoogleDrive via the following [link](https://drive.google.com/drive/folders/16dyzRNrJLe9g0KVpsoaIJhW7-nmf6j1V?usp=sharing).

## Stack Overflow Duplicity Dataset (SODD)

The Stack Overflow Duplicity Dataset (SOD) is a dataset designated for training duplicity detection models. The duplicate question detection task is a very challanging since it requires the model to distinguis tiny semantic nuances. Trained models can then be deployed to Q&A websites such as the Stack Overflow or Quora, where it can improve the users' search experiente by automatically linking and detecting the duplicates. The resulting dataset is based on a StackOverflow data dump acquired from [archive.org](https://archive.org/download/stackexchange) in June 2020.

**Download the dataset:**

The SODD dataset can be obtained from our GoogleDrive via the following [link](https://drive.google.com/drive/folders/1JG6Fibvhs0Jz6JD83gwMqAmzUV9rsoX3?usp=sharing).

**Data Structure**

The dataset is split into train/dev/test splits and is stored in _parquet_ files compressed using _gzip_. The data can be loaded using _pandas_ library using the following code snippet:

```Python
!pip3 install pandas pyarrow

import pandas as pd

train_df = pd.read_parquet('SODD_train.parquet.gzip')
dev_df = pd.read_parquet('SODD_dev.parquet.gzip')
test_df = pd.read_parquet('SODD_test.parquet.gzip')
```

The dataframe loaded using the snippet above contain the following columns:

* **first_post** - HTML formatted data of the first question (contains both text and code snippets)
* **second_post** - HTML formatted data of the second question (contains both text and code snippets)
* **first_author** - username of the first question's author
* **second_author** - username of the second question's author
* **label** - label determining the relationship of the two questions
     * 0 - duplicates
     * 1 - similar based on fulltext search
     * 2 - similar based on tags
     * 3 - different
     * 4 - accepted answer
* **page** - Stack Exchange page from which the questions originate (always set to `stackoverflow`)

**Dataset Size:**

The following table provides detailed information about the dataset size. The table does not consider pairs with label `4 - accepted answer`. Those examples are not utilized in our paper, but we include them in the dataset to open up other possibilities of using our dataset.


| **Type**       | **Train** | **Dev**  | **Test** | **Total** |
|------------|-------|------|------|-------|
| Different  | 550K  | 64K  | 32K  | 646K  |
| Similar    | 526K  | 62K  | 30K  | 618K  |
| Duplicates | 191K  | 22K  | 11K  | 224K  |
| Total      | 1.2M  | 148K | 73K  | 1.4M  |

## Licence
This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. http://creativecommons.org/licenses/by-nc-sa/4.0/

## How should I cite the MQDD? 
For now, please cite [the Arxiv paper](https://arxiv.org/abs/xxx):
```
@article{pasekj2022mqdd,
      title={MQDD -- Pre-training of Multimodal Question Duplicity Detection for Software Engineering Domain}, 
      author={Jan Pašek and Jakub Sido and Miloslav Konopík and Ondřej Pražák},
      year={2022},
      eprint={TODO},
      archivePrefix={TODO},
      primaryClass={TODO},
      journal={TODO},
}
```
