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
```