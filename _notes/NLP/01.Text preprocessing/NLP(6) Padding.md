---
title: NLP(6) Padding
feed: hide
date: 05-08-2024
---
#### Posting information

- Posting Date : 05-08-2024  
- Last Edit : 05-08-2024  
- Writer : KWON Bongjae

#### Posting detail

```
#01_06 : Padding

  

import numpy as np

from tensorflow.keras.preprocessing.text import Tokenizer

  

preprocessed_sentences = [['pooh', 'robin'], ['pooh', 'friend', 'robin'], ['pooh', 'likes', 'robin'], ['love', 'honey'], ['honey', 'home', 'likes', 'honey'], ['likes', 'honey'], ['pooh', 'home', 'word'], ['pooh', 'home', 'word'], ['pooh', 'home', 'honey'], ['keeping', 'keeping', 'likes', 'honey', 'driving', 'pooh', 'village'], ['pooh', 'went', 'likes', 'mountain']]

  

tokenizer = Tokenizer()

tokenizer.fit_on_texts(preprocessed_sentences)

encoded = tokenizer.texts_to_sequences(preprocessed_sentences)

print(encoded)

#[[1, 5], [1, 8, 5], [1, 3, 5], [9, 2], [2, 4, 3, 2], [3, 2], [1, 4, 6], [1, 4, 6], [1, 4, 2], [7, 7, 3, 2, 10, 1, 11], [1, 12, 3, 13]]

  

max_len = max(len(item) for item in encoded)

print('max length :', max_len)

#max length : 7

  

for sentence in encoded:

while len(sentence) < max_len:

sentence.append(0)

  

padded_np = np.array(encoded)

print(padded_np)

'''

[[ 1 5 0 0 0 0 0]

[ 1 8 5 0 0 0 0]

[ 1 3 5 0 0 0 0]

[ 9 2 0 0 0 0 0]

[ 2 4 3 2 0 0 0]

[ 3 2 0 0 0 0 0]

[ 1 4 6 0 0 0 0]

[ 1 4 6 0 0 0 0]

[ 1 4 2 0 0 0 0]

[ 7 7 3 2 10 1 11]

[ 1 12 3 13 0 0 0]]

'''

  
  

#Padding in keras

  

from tensorflow.keras.preprocessing.sequence import pad_sequences

  

encoded = tokenizer.texts_to_sequences(preprocessed_sentences)

print(encoded)

  

padded = pad_sequences(encoded)

print(padded)

'''

[[ 0 0 0 0 0 1 5]

[ 0 0 0 0 1 8 5]

[ 0 0 0 0 1 3 5]

[ 0 0 0 0 0 9 2]

[ 0 0 0 2 4 3 2]

[ 0 0 0 0 0 3 2]

[ 0 0 0 0 1 4 6]

[ 0 0 0 0 1 4 6]

[ 0 0 0 0 1 4 2]

[ 7 7 3 2 10 1 11]

[ 0 0 0 1 12 3 13]]

'''

  

padded = pad_sequences(encoded, padding = 'post')

print(padded)

'''

[[ 1 5 0 0 0 0 0]

[ 1 8 5 0 0 0 0]

[ 1 3 5 0 0 0 0]

[ 9 2 0 0 0 0 0]

[ 2 4 3 2 0 0 0]

[ 3 2 0 0 0 0 0]

[ 1 4 6 0 0 0 0]

[ 1 4 6 0 0 0 0]

[ 1 4 2 0 0 0 0]

[ 7 7 3 2 10 1 11]

[ 1 12 3 13 0 0 0]]

'''

  

print((padded == padded_np).all())

#Ture

  

padded = pad_sequences(encoded, padding= 'post', maxlen=5)

print(padded)

'''

[[ 1 5 0 0 0]

[ 1 8 5 0 0]

[ 1 3 5 0 0]

[ 9 2 0 0 0]

[ 2 4 3 2 0]

[ 3 2 0 0 0]

[ 1 4 6 0 0]

[ 1 4 6 0 0]

[ 1 4 2 0 0]

[ 3 2 10 1 11]

[ 1 12 3 13 0]]

'''

  

padded = pad_sequences(encoded, padding= 'post', truncating='post', maxlen=5)

print(padded)

'''

[[ 1 5 0 0 0]

[ 1 8 5 0 0]

[ 1 3 5 0 0]

[ 9 2 0 0 0]

[ 2 4 3 2 0]

[ 3 2 0 0 0]

[ 1 4 6 0 0]

[ 1 4 6 0 0]

[ 1 4 2 0 0]

[ 7 7 3 2 10]

[ 1 12 3 13 0]]

'''

  

last_value = len(tokenizer.word_index) + 1

print(last_value)

#14

  

padded = pad_sequences(encoded, padding= 'post', truncating='post', value=last_value)

print(padded)

'''

[[ 1 5 14 14 14 14 14]

[ 1 8 5 14 14 14 14]

[ 1 3 5 14 14 14 14]

[ 9 2 14 14 14 14 14]

[ 2 4 3 2 14 14 14]

[ 3 2 14 14 14 14 14]

[ 1 4 6 14 14 14 14]

[ 1 4 6 14 14 14 14]

[ 1 4 2 14 14 14 14]

[ 7 7 3 2 10 1 11]

[ 1 12 3 13 14 14 14]]

'''
```