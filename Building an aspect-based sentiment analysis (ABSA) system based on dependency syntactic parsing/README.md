# Building an aspect-based sentiment analysis (ABSA) system based on dependency syntactic parsing

This project is to build an aspect-based sentiment analysis (ABSA) system based on syntactic parsing. The aspect-based sentiment analysis try to analyse the sentiment, e.g., positive, negative and neutral, toward a given aspect (aspect term). In order to complete this project, steps are: 

1) reading data from the dataset file (.xml) to dictionary and performing text pre-processing such as converting characters into lower case characters and removing stop words etc., 

2) perform parsing such as dependency parsing on the sentence 

3) designing rules based on syntactic parsing results for 3 sentiments 

4) Calculating the Precision and Recall for each rule for evaluation. A Jupyter Notebook with Python kernel is used to work on this project.

# Dataset
![pic1](https://user-images.githubusercontent.com/57484350/177001793-9afc1898-74b3-472f-95f1-65afca256d5d.jpg)

The dataset (Restaurant.xml) used in this project is a collection of reviews on restaurant, including their food, service etc. It contains fields like sentence id, sentence text, aspect term, aspect term polarity, aspect term span, aspect category, aspect category polarity. And only sentence text, aspect term and aspect term polarity need to be considered.


# Procedure
<li> Exploratory data analysis
<li> Data Preprocessing
<li> Appling Dependency Parsing on reviews
<li> Building Aspect Term Based Rules for positive/neutral/negative reviews
<li> Evaluation for various Aspect Term Based Rules

# Methodology

## Dependency Parsing

Dependency Parsing is the process to analyze the grammatical structure in a sentence and find out related words as well as the type of the relationship between them. The syntactic structure of a sentence is described solely in terms of directed binary grammatical relations between the words, as in the following dependency parse: Relations among the words are illustrated above the sentence with directed, labeled arcs from heads to dependents. We call this a typed dependency structure because typed dependency the labels are drawn from a fixed inventory of grammatical relations. A root node explicitly marks the root of the tree, the head of the entire structure.
