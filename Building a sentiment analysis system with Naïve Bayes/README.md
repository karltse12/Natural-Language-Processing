# Building a sentiment analysis system with Naïve Bayes

This project requires us to build a sentiment analysis system on the given dataset – IMDB Movie review. We have to train a natural language processing (NLP) model based on the Naïve Bayes classifier to distinguish whether the review is positive or negative. A set of 25,000 highly polar movie reviews for training and 25,000 for testing procided. The goal is to figure out some ways to predict the correct sentiment, as well as maximize the F1 score.

Data Download Link: https://www.kaggle.com/datasets/lakshmi25npathi/imdb-dataset-of-50k-movie-reviews

# Major Challenge
The major challenge of this project is to build the sentiment analysis system with Naïve Bayes from scratch. Third party libraries are NOT allowed for construction of Naïve Bayes classifier and F1 measure calculation. 

# Attributes
| Column ID |         Column Name        | Data type |       Description         |
|:---------:|:--------------------------:|:---------:|:-------------------------:|
|     0     |           review           |   int64   |         review            |
|     1     |           label            |   object  |     positive/negative     |


# Implemetation

### Data Pre-Processing

First of all, use pandas to read the csv file and choose 2 columns (review, label) and place
them into pandas dataframe. Then, remove all the unlabelled samples by filtering out all the rows.
After that, use the regular expression to remove all the remove non-English characters from
review. Then, change all the characters in review to lower case. Then, split the review into the list
of words, that means all single words in the review become the elements of the list.
Import the Natural Language Toolkit library (nltk), remove all the non-English words in the list,
and remove all the stopword (which means the words which does not add much meaning to a
sentence). Also, apply the text normalization techniques such as stemming, lemmatization to
achieve the root forms of words in the same family. Finally, join all the words in the list into one
sentence.
Create 2 more dataframes to hold the training data (25,000 rows) and testing data (25,000 rows)
separately.

### Build a Naïve Bayes Classifier from scratch

There are 2 parts in Naïve Bayes classifier.

#### 1) Prior Probability

![formula1](https://user-images.githubusercontent.com/57484350/176993386-736a6864-34fd-4f46-bd89-5c820a9cebfc.PNG)

For the 1st part, I have to create a probability for each class (positive & negative). In
order to do this, both the number of positive reviews and negative reviews are counted. The prior
probability represents the underlying probability in the target set that a review is positive or
negative. Since the denomiator of probability for each class are the same, so the prior probability
can be calculated simply by (number of positive reviews/number of negative reviews).


#### 2) Word Probability and Sentence Probaility
![formula2](https://user-images.githubusercontent.com/57484350/176993409-d33ca9f4-e6cd-418b-a436-ca6405b63da7.PNG)

For the 2nd part, I created the dictionary of frequencies of both distinct positive
words and distinct negative words (keys are distinct word, and the values are their frequencies),
and this is the count(wk, c) in the above right formula. For the denominator of right formula, the
summation of count(w, c) is equal to total number of distinct words for that class (either positive
or negative) and the ‘V’ is equal to total number of distinct words. Therefore, the probability of a
single word P(wk|c) can be calculated. Since zero probability of one word P(wk|c) = 0 will make
the whole sentence probability zero, so we will use smoothing by adding 1 to the Numerator and
adding |V| to the denominator. After calculating each single word probability, we can calculate
the whole review sentence probability simply multiply all the single word probability together.

### Logrithm

In order to reduce the computational cost, the logrithm will be introduced to both formula,
therefore there will be log(prior probability) and log(sentence probaility). Orignally, there are a
lot of multiplications inside the sentence probaility, which cost a lot of running time. After
applying the logrithm, multiplication operations will become addition operation, and this saves a
lot of running time.

### Adopt different k value for k smoothing for building the Naïve Bayes Classifier
![formula3](https://user-images.githubusercontent.com/57484350/176993877-3553d7f6-33b3-4506-a8c2-74c41cf019df.PNG)

K smoothing is a technique that tackles the problem of zero probability in Naïve Bayes algorithm.
In the below formula, k represents the smoothing parameter. Instead of using k = 1 (in first experiment), k =2 and k =3 are used as smoothing parameter to see how it affects the performance of sentiment analysis system.

# Text normalization Used

### Lemmatization

In computational linguistics, lemmatisation is the algorithmic process of determining the lemma
of a word based on its intended meaning. Unlike stemming, lemmatisation depends on correctly
identifying the intended part of speech and meaning of a word in a sentence, as well as within the
larger context surrounding that sentence. , such as neighboring sentences or even an entire
document. As a result, developing efficient Lemmatisation algorithms is an open area of research.

### Porter Stemmer

The Porter stemming algorithm (or ‘Porter stemmer’) is a process for removing the commoner
morphological and inflexional endings from words in English. Its main use is as part of a term
normalisation process that is usually done when setting up Information Retrieval systems. [2]
Stemming is a crude way of performing lemmatization, it chops off word-final stemming affixes.

###  Snowball Stemmer

Many implementations of the Porter stemming algorithm were written and freely distributed;
however, many of these implementations contained subtle flaws. As a result, these stemmers did
not match their potential. To eliminate this source of error, Martin Porter released an official free
software (mostly BSD-licensed) implementation of the algorithm around the year 2000. He
extended this work over the next few years by building Snowball, a framework for writing
stemming algorithms, and implemented an improved English stemmer together with stemmers
for several other languages.

