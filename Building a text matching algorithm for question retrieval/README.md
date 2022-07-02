# Building a text matching algorithm for question retrieval

This project is to build a text retrieval/matching system to matching similar questions. This can be done by training natural language processing (NLP) models based on 3 different algorithms, which are TF-IDF (Term Frequency times Inverse Document Frequency), Sentence Embedding (by averaging word embedding) and Sentence Embedding (by down weight frequent words). 

In order to complete this project, steps are: 1) reading data from the dataset file (.tsv) and performing text pre-processing such as removing punctuation, stemming, removing stop words etc., 2) building inverted index with TF-IDF from scratch and performing text matching, 3) building text matching with sentence embedding (averaging word embedding) by pretrained model and performing text matching, 4) building text matching with sentence embedding (down weight frequent words) by pretrained model and performing text matching. For each algorithm, performance is evaluated by counting the number of matches ranked top2 and top5 within first 100 queries. The higher the number of matches, the better the performance of the algorithm. A Jupyter Notebook with Python kernel is used to work on this project.

# Major Challenge
The major challenge of this project is to build the TF-IDF from scratch. Third party libraries are NOT allowed for construction of TF-IDF. Also, algorithmic efficiency is a challenge for this project since there are around 400,000 rows of data.


# Dataset
![image](https://user-images.githubusercontent.com/57484350/176996065-7d32b728-a6b8-455d-a408-91bdfc035ad0.png)

| Column ID |         Column Name        | Data type |       Description         |
|:---------:|:--------------------------:|:---------:|:-------------------------:|
|     0     |           Id               |   object  |        Unique ID          |
|     1     |           qid1             |   object  |   Unique ID of question1  |
|     2     |           qid2             |   float64 |   Unique ID of question2  |
|     3     |           question1        |   object  |        question1          |
|     4     |           question2        |   object  |        question2          |
|     5     |           is_duplicate     |   float64 |    whether question1 is similar to question2 |

# Procedure

<li> Exploratory data analysis
<li> Data Preprocessing
<li> Text Cleansing
<li> Building text matching with TF-IDF based by scratch
<li> Building text matching with sentence embedding (averaging word embedding) by pretrained model
<li> Building text matching with sentence embedding (down weight frequent words) by pretrained model
<li> Comparison & Evaluation for 3 diiferent models

# Methodology

### TF-IDF Based (with inverted index)

TF-IDF is short for term frequency–inverse document frequency, is a numerical statistic that is intended to reflect how important a word is to a document in a collection or corpus. It is often used as a weighting factor in searches of information retrieval, text mining, and user modeling. The mechanism of TF-IDF is to increase the weight of important words and decrease the weight of irrelevant words.

TF-IDF = Term Frequency (TF) * Inverse Document Frequency (IDF)

#### Term Frequency (TF)

The number of times a term (t) occurs in a document (d) is called its term frequency. Say like the document only contains 3 words e.g. ‘green tea latte’. According to the formula in notes, the term frequency of ‘green’ in this document is equal to log(1+1) = log2.

#### Inverse Document Frequency (IDF)

The Term Frequency only emphasizes on a specific document. For TF-IDF, words that occur much more frequently is less meaningful. Therefore, IDF is used to decrease the weight of frequency words. According to notes, the document frequency (DF) of a term t is simply the number documents it occurs. And the Inverse Document Frequency is calculated by number of documents (N)/ document frequency (DF). For example, there are total 10 documents, and 5 of them contain the word ‘green’, then the IDF of ‘green’ is equal to 10/5 = 2.

#### Inverted Index

An inverted index is an index data structure storing a mapping from content, such as words or numbers, to its locations in a document or a set of documents. In simple words, it is a hashmap like data structure that directs you from a word to a document. It is called Inverted file because it collects the occurrence information of each word in different documents. Simply to say, each word can be seen as a ‘document’. In order to find the similar query, first the query will be broken down into words. For each word, the document that contains the word are found, and the related TF-IDF is calculated. Finally, rank the documents by the accumulated TF-IDF. The higher the accumulated TF-IDF, the higher the similarity with the query.
