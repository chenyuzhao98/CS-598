# CS 598 Final Project

> Update: Deleted data/annotations.csv, which contains small parts of MIMIC data

## Team Information
- Group ID: 112
- Paper ID: 163
- Teammate 1: Chenyu Zhao (chenyu5)
- Teammate 2: Ashley Xu (ziqixu3)

## Citation to Original Paper

Gehrmann S, Dernoncourt F, Li Y, Carlson ET, Wu JT, Welt J, Foote J Jr, Moseley ET, Grant DW, Tyler PD, Celi LA. Comparing deep learning and concept extraction based methods for patient phenotyping from clinical narratives. PLoS One. 2018 Feb 15;13(2):e0192360. doi: 10.1371/journal.pone.0192360. PMID: 29447188; PMCID: PMC5813927.

## Original Paper's Codebase

Please refer to author Sebastian Gehrmann's [GitHub repo](https://github.com/sebastianGehrmann/phenotyping).

## Dependencies

Since this paper was published 6 years ago, please make sure you are using `Python2.7`. You can refer to `requirements.txt` for a complete list of dependencies with versioning information, or simply bulk install all dependencies by running: 
```python
$ pip install -r requirements.txt
```

## Data Acquisition 

In `data/annotations_wo_text.csv`, you can find our annotations as well as unique identifiers for patient visits in MIMIC-III, namely the hospital admission ID, subject ID, and chart time. Due to HIPAA requirements, we cannot provide the text of the patients' discharge summary in this repository.  

You can find the discharge summary from the MIMIC-III `NOTEEVENTS` table, which can be accessed at https://mimic.mit.edu/docs/iii/tables/noteevents/. Please take note that legitimate PhysioNet credential is needed to download the dataset. 

## Prepocessing
1. Once you accquired the MIMIC-III `NOTEEVENTS` table, you need to combine `NOTEEVENTS`'s  discharge summary with the provided `data/annotations_wo_text.csv` dataset. You can refer to `598_Project.ipynb` for detailed implementation on merging the two datasets. The resulting dataset is stored at `data/annotations.csv`
2. Prepare a word2vec file on the extracted texts. You can find our pre-made word2vec vectors in `data/w2v.txt.zip`. Please unzip the file first before proceeding.
3. You would need to perform text prepocessing on the dataset (string split, remove stop words and punctuations, string vectorization, etc). This can be done by running the following command with `Python 2.7`:
 ```
python preprocess.py data/annotations.csv w2v.txt
 ```

## Training
If the preprocessing step succeeded, you would see a new file `data-nobatch.h5` in your main directory. If that is the case, you can run the following command to start the model training process:
```
python ngram_models.py --data data-nobatch.h5 --ngram <x>
```
Please substitute `<x>` with your desired n-gram number. In our case, we tried 1~5.  

## Table of results

![alt text](https://github.com/chenyuzhao98/CS-598/blob/main/table1.jpg?raw=true)
![alt text](https://github.com/chenyuzhao98/CS-598/blob/main/table2.jpg?raw=true)
![alt text](https://github.com/chenyuzhao98/CS-598/blob/main/table3.jpg?raw=true)
![alt text](https://github.com/chenyuzhao98/CS-598/blob/main/accuracy.png?raw=true)
![alt text](https://github.com/chenyuzhao98/CS-598/blob/main/f1.png?raw=true)
