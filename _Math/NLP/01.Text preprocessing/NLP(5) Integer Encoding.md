---
title: NLP(5) Integer Encoding
feed: show
date: 04-08-2024
---
#### Posting information

- Posting Date : 04-08-2024  
- Last Edit : 05-08-2024  
- Writer : KWON Bongjae

#### Posting detail

```
#01_05 : Integer Encoding

  

#1) using dictionary

from nltk.tokenize import sent_tokenize

from nltk.tokenize import word_tokenize

from nltk.corpus import stopwords

  

raw_text = """Edward Bear, known to his friends as Winnie-the-Pooh, or Pooh for

short, was walking through the forest one day, humming proudly to

himself. Pooh had made up a little hum that very morning, as Pooh was doing

his Stoutness Exercises in front of the glass: _Tra-la-la, tra-la-la_,

as he stretched up as high as he could go, and then _Tra-la-la,

tra-la--oh, help!--la_, as he tried to reach his toes."""

  

sentences = sent_tokenize(raw_text)

print(sentences)

#['Edward Bear, known to his friends as Winnie-the-Pooh, or Pooh for\nshort, was walking through the forest one day, humming proudly to\nhimself.', 'Pooh had made up a little hum that very morning, as Pooh was doing\nhis Stoutness Exercises in front of the glass: _Tra-la-la, tra-la-la_,\nas he stretched up as high as he could go, and then _Tra-la-la,\ntra-la--oh, help!--la_, as he tried to reach his toes.']

  

vocab = {} #dictionary

preprocessed_sentences = [] #list

stop_words = set(stopwords.words('english'))

  

for sentence in sentences :

tokenized_sentence = word_tokenize(sentence)

result = []

  

for word in tokenized_sentence :

word = word.lower()

  

if word not in stop_words:

if len(word) > 2:

result.append(word)

if word not in vocab:

vocab[word] = 0

vocab[word] += 1

preprocessed_sentences.append(result)

  

print(preprocessed_sentences)

#[['edward', 'bear', 'known', 'friends', 'winnie-the-pooh', 'pooh', 'short', 'walking', 'forest', 'one', 'day', 'humming', 'proudly'], ['pooh', 'made', 'little', 'hum', 'morning', 'pooh', 'stoutness', 'exercises', 'front', 'glass', '_tra-la-la', 'tra-la-la_', 'stretched', 'high', 'could', '_tra-la-la', 'tra-la', 'help', 'la_', 'tried', 'reach', 'toes']]

  

print('Vocab :', vocab)

#Vocab : {'edward': 1, 'bear': 1, 'known': 1, 'friends': 1, 'winnie-the-pooh': 1, 'pooh': 3, 'short': 1, 'walking': 1, 'forest': 1, 'one': 1, 'day': 1, 'humming': 1, 'proudly': 1, 'made': 1, 'little': 1, 'hum': 1, 'morning': 1, 'stoutness': 1, 'exercises': 1, 'front': 1, 'glass': 1, '_tra-la-la': 2, 'tra-la-la_': 1, 'stretched': 1, 'high': 1, 'could': 1, 'tra-la': 1, 'help': 1, 'la_': 1, 'tried': 1, 'reach': 1, 'toes': 1}

  

print(vocab["pooh"])

#3

  

vocab_sorted = sorted(vocab.items(), key = lambda x:x[1], reverse = True)

print(vocab_sorted)

#[('pooh', 3), ('_tra-la-la', 2), ('edward', 1), ('bear', 1), ('known', 1), ('friends', 1), ('winnie-the-pooh', 1), ('short', 1), ('walking', 1), ('forest', 1), ('one', 1), ('day', 1), ('humming', 1), ('proudly', 1), ('made', 1), ('little', 1), ('hum', 1), ('morning', 1), ('stoutness', 1), ('exercises', 1), ('front', 1), ('glass', 1), ('tra-la-la_', 1), ('stretched', 1), ('high', 1), ('could', 1), ('tra-la', 1), ('help', 1), ('la_', 1), ('tried', 1), ('reach', 1), ('toes', 1)]

  

word_to_index = {}

i = 0

for (word, frequency) in vocab_sorted:

if frequency > 1 :

i = i + 1

word_to_index[word] = i

  

print(word_to_index)

#{'pooh': 1, '_tra-la-la': 2}

  

vocab_size = 1

words_frequency = [word for word, index in word_to_index.items() if index >= vocab_size + 1 ]

  

for w in words_frequency:

del word_to_index[w]

print(word_to_index)

#{'pooh': 1}

  
  

word_to_index['OOV'] = len(word_to_index) + 1 #Out-Of-Vocabulary

print(word_to_index)

#{'pooh': 1, 'OOV': 2}

  

encoded_sentences = []

for sentence in preprocessed_sentences:

encoded_sentences = []

for word in sentence:

try:

encoded_sentences.append(word_to_index[word])

except KeyError:

encoded_sentences.append(word_to_index['OOV'])

  
  

encoded_sentences.append(encoded_sentences)

print(encoded_sentences)

#[1, 2, 2, 2, 2, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, [...]] ***?

  
  

#2) Counter

  

from collections import Counter

print(preprocessed_sentences)

#[['edward', 'bear', 'known', 'friends', 'winnie-the-pooh', 'pooh', 'short', 'walking', 'forest', 'one', 'day', 'humming', 'proudly'], ['pooh', 'made', 'little', 'hum', 'morning', 'pooh', 'stoutness', 'exercises', 'front', 'glass', '_tra-la-la', 'tra-la-la_', 'stretched', 'high', 'could', '_tra-la-la', 'tra-la', 'help', 'la_', 'tried', 'reach', 'toes']]

  

all_words_list = sum(preprocessed_sentences, [])

print(all_words_list)

#['edward', 'bear', 'known', 'friends', 'winnie-the-pooh', 'pooh', 'short', 'walking', 'forest', 'one', 'day', 'humming', 'proudly', 'pooh', 'made', 'little', 'hum', 'morning', 'pooh', 'stoutness', 'exercises', 'front', 'glass', '_tra-la-la', 'tra-la-la_', 'stretched', 'high', 'could', '_tra-la-la', 'tra-la', 'help', 'la_', 'tried', 'reach', 'toes']

  

vocab = Counter(all_words_list)

print(vocab)

#Counter({'pooh': 3, '_tra-la-la': 2, 'edward': 1, 'bear': 1, 'known': 1, 'friends': 1, 'winnie-the-pooh': 1, 'short': 1, 'walking': 1, 'forest': 1, 'one': 1, 'day': 1, 'humming': 1, 'proudly': 1, 'made': 1, 'little': 1, 'hum': 1, 'morning': 1, 'stoutness': 1, 'exercises': 1, 'front': 1, 'glass': 1, 'tra-la-la_': 1, 'stretched': 1, 'high': 1, 'could': 1, 'tra-la': 1, 'help': 1, 'la_': 1, 'tried': 1, 'reach': 1, 'toes': 1})

  

print(vocab["pooh"])

#3

  

vocab_size = 3

vocab = vocab.most_common(vocab_size)

print(vocab)

#[('pooh', 3), ('_tra-la-la', 2), ('edward', 1)]

  

word_to_index = {}

i = 0

for (word, frequency) in vocab :

i = i + 1

word_to_index[word] = i

  

print(word_to_index)

#{'pooh': 1, '_tra-la-la': 2, 'edward': 3}

  
  

#FreqDist in NLTK

  

from nltk import FreqDist

import numpy as np

  

vocab = FreqDist(np.hstack(preprocessed_sentences))

  

print(vocab["pooh"])

#3

  

vocab_size = 3

vocab = vocab.most_common(vocab_size)

print(vocab)

#[('pooh', 3), ('_tra-la-la', 2), ('edward', 1)]

  

word_to_index = {word[0] : index + 1 for index, word in enumerate(vocab)}

print(word_to_index)

#{'pooh': 1, '_tra-la-la': 2, 'edward': 3}

  
  

#enumerate

test_input = ['a', 'b', 'c', 'd', 'e', 'f', 'g']

for index, value in enumerate(test_input):

print("value : {}, index: {}".format(value, index))

"""

value : a, index: 0

value : b, index: 1

value : c, index: 2

value : d, index: 3

value : e, index: 4

value : f, index: 5

value : g, index: 6

"""

  
  

#Text preprocessing in keras

  

from tensorflow.keras.preprocessing.text import Tokenizer

  

tokenizer = Tokenizer()

tokenizer.fit_on_texts(preprocessed_sentences)

print(tokenizer.word_index)

#{'pooh': 1, '_tra-la-la': 2, 'edward': 3, 'bear': 4, 'known': 5, 'friends': 6, 'winnie-the-pooh': 7, 'short': 8, 'walking': 9, 'forest': 10, 'one': 11, 'day': 12, 'humming': 13, 'proudly': 14, 'made': 15, 'little': 16, 'hum': 17, 'morning': 18, 'stoutness': 19, 'exercises': 20, 'front': 21, 'glass': 22, 'tra-la-la_': 23, 'stretched': 24, 'high': 25, 'could': 26, 'tra-la': 27, 'help': 28, 'la_': 29, 'tried': 30, 'reach': 31, 'toes': 32}

  

print(tokenizer.word_counts)

#OrderedDict([('edward', 1), ('bear', 1), ('known', 1), ('friends', 1), ('winnie-the-pooh', 1), ('pooh', 3), ('short', 1), ('walking', 1), ('forest', 1), ('one', 1), ('day', 1), ('humming', 1), ('proudly', 1), ('made', 1), ('little', 1), ('hum', 1), ('morning', 1), ('stoutness', 1), ('exercises', 1), ('front', 1), ('glass', 1), ('_tra-la-la', 2), ('tra-la-la_', 1), ('stretched', 1), ('high', 1), ('could', 1), ('tra-la', 1), ('help', 1), ('la_', 1), ('tried', 1), ('reach', 1), ('toes', 1)])

  

print(tokenizer.texts_to_sequences(preprocessed_sentences))

#[[3, 4, 5, 6, 7, 1, 8, 9, 10, 11, 12, 13, 14], [1, 15, 16, 17, 18, 1, 19, 20, 21, 22, 2, 23, 24, 25, 26, 2, 27, 28, 29, 30, 31, 32]]

vocab_size = 3

tokenizer = Tokenizer(num_words = vocab_size +1)

tokenizer.fit_on_texts(preprocessed_sentences)

print(tokenizer.word_index)

#{'pooh': 1, '_tra-la-la': 2, 'edward': 3, 'bear': 4, 'known': 5, 'friends': 6, 'winnie-the-pooh': 7, 'short': 8, 'walking': 9, 'forest': 10, 'one': 11, 'day': 12, 'humming': 13, 'proudly': 14, 'made': 15, 'little': 16, 'hum': 17, 'morning': 18, 'stoutness': 19, 'exercises': 20, 'front': 21, 'glass': 22, 'tra-la-la_': 23, 'stretched': 24, 'high': 25, 'could': 26, 'tra-la': 27, 'help': 28, 'la_': 29, 'tried': 30, 'reach': 31, 'toes': 32}

  

print(tokenizer.texts_to_sequences(preprocessed_sentences))

#[[3, 1], [1, 1, 2, 2]]
```