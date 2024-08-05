---
title: NLP(2) Stemming&Lemmatization
feed: show
date: 02-08-2024
---
#### Posting information

- Posting Date : 02-08-2024  
- Last Edit : 02-08-2024  
- Writer : KWON Bongjae

#### Posting detail

```
#01_02 : Cleaning & Normalization

  

#_01_02_01 : Cleaning

import re

text = """

"Terrible and Sad," said Pooh, "because Eeyore, who is a friend of mine, has lost his tail. And he's Moping about it. So could you very kindly tell me how to find it for him?"

"""

  

# Delete words 1 to 2 in length using regular expressions

#shortword = re.compile(r'\W*\b\w{1,2}\b')

#print(shortword.sub('', text))

#***"Terrible and Sad," said Pooh, "because Eeyore, who friend mine, has lost his tail. And Moping about could you very kindly tell how find for him?"

  
  
  

#_01_02_02 : Lemmatization

  

from nltk.stem import WordNetLemmatizer

  

lemmatizer = WordNetLemmatizer()

  

#words = ['policy', 'doing', 'organization', 'have', 'going', 'love', 'lives', 'fly', 'dies', 'watched', 'has', 'starting']

  

#print('Before Lemmatization :',words)

#print('After Lemmatization :',[lemmatizer.lemmatize(word) for word in words])

  

#Before Lemmatization : ['policy', 'doing', 'organization', 'have', 'going', 'love', 'lives', 'fly', 'dies', 'watched', 'has', 'starting']

#After Lemmatization : ['policy', 'doing', 'organization', 'have', 'going', 'love', 'life', 'fly', 'dy', 'watched', 'ha', 'starting']

  

#print('After Lemmatization :',[lemmatizer.lemmatize('dies', 'v')])

#After Lemmatization : ['die']

  
  

#_01_02_03 : Stemming

  

from nltk.stem import PorterStemmer

from nltk.tokenize import word_tokenize

  

stemmer = PorterStemmer()

  

sentence = """

"I see, I see," said Pooh, nodding his head. "Talking about large

somethings," he went on dreamily, "I generally have a small something

about now--about this time in the morning," and he looked wistfully at

the cupboard in the corner of Owl's parlour; "just a mouthful of

condensed milk or whatnot, with perhaps a lick of honey."

"""

tokenized_sentence = word_tokenize(sentence)

  

print('Before Stemming :', tokenized_sentence)

print('After Stemming :',[stemmer.stem(word) for word in tokenized_sentence])

#Before Stemming : ["''", 'I', 'see', ',', 'I', 'see', ',', "''", 'said', 'Pooh', ',', 'nodding', 'his', 'head', '.', '``', 'Talking', 'about', 'large', 'somethings', ',', "''", 'he', 'went', 'on', 'dreamily', ',', '``', 'I', 'generally', 'have', 'a', 'small', 'something', 'about', 'now', '--', 'about', 'this', 'time', 'in', 'the', 'morning', ',', "''", 'and', 'he', 'looked', 'wistfully', 'at', 'the', 'cupboard', 'in', 'the', 'corner', 'of', 'Owl', "'s", 'parlour', ';', '``', 'just', 'a', 'mouthful', 'of', 'condensed', 'milk', 'or', 'whatnot', ',', 'with', 'perhaps', 'a', 'lick', 'of', 'honey', '.', "''"]

#

# After Stemming : ["''", 'i', 'see', ',', 'i', 'see', ',', "''", 'said', 'pooh', ',', 'nod', 'hi', 'head', '.', '``', 'talk', 'about', 'larg', 'someth', ',', "''", 'he', 'went', 'on', 'dreamili', ',', '``', 'i', 'gener', 'have', 'a', 'small', 'someth', 'about', 'now', '--', 'about', 'thi', 'time', 'in', 'the', 'morn', ',', "''", 'and', 'he', 'look', 'wist', 'at', 'the', 'cupboard', 'in', 'the', 'corner', 'of', 'owl', "'s", 'parlour', ';', '``', 'just', 'a', 'mouth', 'of', 'condens', 'milk', 'or', 'whatnot', ',', 'with', 'perhap', 'a', 'lick', 'of', 'honey', '.', "''"]

  
  

words = ['Normalize', 'Distance', 'electricical']

  

print('Before Stemming :',words)

print('After Stemming :',[stemmer.stem(word) for word in words])

# After Stemming : ['normal', 'distanc', 'electric']

  
  
  

from nltk.stem import PorterStemmer

from nltk.stem import LancasterStemmer

  

porter_stemmer = PorterStemmer()

lancaster_stemmer = LancasterStemmer()

  

words = ['policy', 'doing', 'organization', 'have', 'going', 'love', 'lives', 'fly', 'dies', 'watched', 'has', 'starting']

print('Before Stemming :', words)

print('PorterStemmer:',[porter_stemmer.stem(w) for w in words])

print('LancasterStemmer:',[lancaster_stemmer.stem(w) for w in words])

#PorterStemmer: ['polici', 'do', 'organ', 'have', 'go', 'love', 'live', 'fli', 'die', 'watch', 'ha', 'start']

#LancasterStemmer: ['policy', 'doing', 'org', 'hav', 'going', 'lov', 'liv', 'fly', 'die', 'watch', 'has', 'start']
```