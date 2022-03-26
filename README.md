# Stack Overflow (Duplicity) Dataset

This repository publishes two novel datasets for (pre-)training NLP models applicable for software engineering domain.
The datasets were presented in the paper [MQDD – Pre-training of Multimodal Question Duplicity Detection for Software Engineering Domain](https://arxiv.org/abs/xxx),
which contains detailed information about the datasets.


## Stack Overflow Dataset (SOD)

The Stack Overflow Dataset (SOD) represents a large corpus of natural language-programming language (NL-PR) pairs. The dataset can be leveraged to pre-train multimodal encoders targetting software engineering domain. The dataset's structure (described below) is specifically tailor for our novel pre-training objectives (see our paper) designed for improving duplicate question detection. However, the dataset can be simply transformed into a general parallel corpus can be used in many different ways. The resulting dataset is based on a StackOverflow data dump acquired from [archive.org](https://archive.org/download/stackexchange) in June 2020. For more information see our [paper](https://arxiv.org/abs/xxx)

**Download the dataset:**

The SOD dataset can be obtained from our GoogleDrive via the following [link](https://drive.google.com/drive/folders/16dyzRNrJLe9g0KVpsoaIJhW7-nmf6j1V?usp=sharing).

**Data Structure**

The Stack Overflow Dataset (SOD) consists of a metadata file and several data files. Each line of the metadata file (`dataset_meta.csv`) contains a JSON array with the following information:

- `question_id` - identifier of the question in format `<id>-<page>` (in our case the `page` = `stackoverflow`)
- `answer_id` - identifier of the answer in format `<id>-<page>` (in our case the `page` = `stackoverflow`)
- `title` - title of the question
- `tags` - tags associated with the question
- `is_answered` - boolean flag indicating whether the answer represents an accepted answer for the question

The dataset export is organized in such a way that `i`-th row in the metadata file corresponds to training examples located on the `i`-th row in the data files. There are six different data file types, each comprising training examples of different _input pair types_. A complete list of the data file types follows:

- `dataset_AC_AT.csv` - code from an answer with text from the same answer
- `dataset_QC_AC.csv` - code from a question with code from a related answer 
- `dataset_QC_AT.csv` - code from a question with text from a related answer
- `dataset_QC_QT.csv` - code from a question with text from the same question
- `dataset_QT_AC.csv` - text from a question with code from a related answer
- `dataset_QT_AT.csv` - text from a question with text from a related answer

Each row in the data file then represents a single example whose metadata can be obtained from a corresponding row in the metadata file. A training example is represented by a JSON array containing two strings. For example, in the `dataset_QC_AC.csv`, the first element in the array contains code from a question, whereas the second element contains code from the related answer. It shall be noted that the dataset export does not contain negative examples since they would significantly increase the disk space required for storing the dataset. The negative examples must be randomly sampled during pre-processing (Section 3.1 in our paper).

Since the resulting dataset takes up a lot of disk space, we split the individual data files and the metadata file into nine smaller ones. Therefore, files such as, for example, `dataset_meta_1.csv` and corresponding `dataset_QC_AT_1.csv` can then be found in the repository.

**Dataset Statistics:**

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

## Contact us

In case of any questions do not hesitate to contact us using email `pasekj{at}ntis.zcu.cz`.

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
