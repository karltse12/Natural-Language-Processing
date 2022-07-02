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

#### Dependency Relations

The traditional linguistic notion of grammatical relation provides the basis for the grammatical relation binary relations that comprise these dependency structures. The arguments to these head relations consist of a head and a dependent. There, the head word of a constituent was the central organizing word of a larger constituent (e.g, the primary noun in a noun phrase, or verb in a verb phrase). The remaining words in the constituent are either direct, or indirect, dependents of their head. In dependency-based approaches, the head-dependent relationship is made explicit by directly linking heads to the words that are immediately dependent on them, bypassing the need for constituent structures.
  
Below graph show some of the dependency relations:

![pic2](https://user-images.githubusercontent.com/57484350/177001857-5ef2d171-5d81-4757-8f13-0dd900ea67e4.JPG)
  
Example Sentence: ‘The boy is clever.’
  
![pic3](https://user-images.githubusercontent.com/57484350/177001878-0ab81ae9-07ac-4aff-a740-6fb28a063fda.JPG)

In this example, each word in the sentence will be tokenized, and each token will have their corresponding head and children, their relation and part of speech are also listed. For example, the token ‘boy ‘, its head is ‘is’ and its children is ‘the’. The relation of ‘boy’ is ‘nsubj’ which means nominal object.
  
In this project, 3rd party library is allowed for performing parsing. spaCy is used in this project, it is an open-source Python library for Natural Language Processing. To get started, first install spaCy and load the required language model (en_core_web_sm). Since there are only total 2021 reviews and only 3602 aspect terms, therefore the smallest English model should be enough for this project. Then, process the sentence text by using the library and the language model. Then, all the relation, part of speech, head and children are generated in the model, just like above example (graph).
  
