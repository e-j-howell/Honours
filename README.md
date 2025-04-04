# Linguistic Analyisis Code

This is a reproducable tool suitable for conducting linguistic analysis on a large text file. In the process of developing this tool it was catered specifically to a study of the language being used in discussion of determinism in academic, popular, and social media. This repository contains the raw data used for this research, as well as the code used to analyse three different data sets of a respective 'academic literature' 'media articles' or 'youtube transcripts' source.

Below is a flow chart to visualise the key processes involved in this tool, followed by a general step-by-step breakdown of how each step is achieved within the code.

![flow chart new](https://github.com/user-attachments/assets/7e145267-98f1-480f-9321-fc76abbe43fb)


## 1. Import Appropriate Tools

```
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from collections import Counter
import string
import nltk
nltk.download('wordnet')
from nltk.stem import WordNetLemmatizer
```

## 2. Read in Text File
```
filename = '50 academic papers.txt'
f = open(filename,encoding = "utf-8")
data = f.read()
```
## 3. Prepare Data
To prepare the data for quantitative analysis, the following factors are considered:
### a. Case
Transforming the data to lowercase creates consistency.
```
datalower = data.lower()
```
### b. Punctuation
Removing punctuation further cleans up the data.
```
# Function to remove punctuation
def remove_punctuation(text):
    return text.translate(str.maketrans('', '', string.punctuation))
text_no_punctuation = remove_punctuation(datalower)
```
### c. Split Data
This tells python to identify each word in the text file as an individual data unit.
```
words = text_no_punctuation.split()
```
### d. Stop Words
This prevents the most common and basic words in the language from dominating the word count results.
```

# Basic list of stop words, expanded upon based on your needs.
stop_words = set([
    "i", "me", "my", "myself", "we", "our", "ours", "ourselves", "you", "your", 
    "yours", "yourself", "yourselves", "he", "him", "his", "himself", "she", 
    "her", "hers", "herself", "it", "its", "itself", "they", "them", "their", 
    "theirs", "themselves", "what", "which", "who", "whom", "this", "that", 
    "these", "those", "am", "is", "are", "was", "were", "be", "been", "being", 
    "have", "has", "had", "having", "do", "does", "did", "doing", "a", "an", 
    "the", "and", "but", "if", "or", "because", "as", "until", "while", "of", 
    "at", "by", "for", "with", "about", "against", "between", "into", "through", 
    "during", "before", "after", "above", "below", "to", "from", "up", "down", 
    "in", "out", "on", "off", "over", "under", "again", "further", "then", 
    "once", "here", "there", "when", "where", "why", "how", "all", "any", 
    "both", "each", "few", "more", "most", "other", "some", "such", "no", 
    "nor", "not", "only", "own", "same", "so", "than", "too", "very", "s", "t", 
    "can", "will", "just", "don", "should", "now", "and", "And", "1", "i'm", 
    "im", "us", "–", "said", "also"
])

# Function to remove stop words
def remove_stop_words(words):
    return [word for word in words if word not in stop_words]
words_no_stop_words = remove_stop_words(words)
```
### e. Lemmatisation
Lemmatisation is a data alteration process essential for many Natural Language Processing tasks. Word forms are reduced to their “lemmata”; simple form. It is important to accurately represent the true prevalance of each key theme or word, rather than have it distributed across many similar forms of the same word.
```
lemmatizer = WordNetLemmatizer()
lemmatized_words = [lemmatizer.lemmatize(word) for word in words_no_stop_words]
```
## 4. Word Counter
This creates a frequency count of each word in the data set.
```
words_count = Counter()
for word in modified_list:
    words_count.update({word,1})
```
## 5. Top 50
This organises the word count to display the top 51 most commonly used words. The reason 51 is used rather than 50, is because the top output will display as the number '1' and its frequency indicates the total number of words in the cleaned and prepared data set.
```
most_common_words = words_count.most_common(51)
```

## 6. Plot
Then, data was plotted from the most frequently used word onwards to create a meaningful and legible graph.

```
x, y = zip(*most_common_words)
plt.bar(x[1:],y[1:])
plt.xticks(rotation=90, fontsize=8)
plt.xlabel('Word')
plt.ylabel('Number of Usages')
plt.title('Most Common Words Used In Positive Media on Organic Produce')
plt.show()
```
