---
title: NLP(7) One Hot Encoding
feed: show
date: 05-08-2024
---
#### Posting information

- Posting Date : 05-08-2024  
- Last Edit : 05-08-2024  
- Writer : KWON Bongjae

#### Posting detail

```
from konlpy.tag import Okt

  

okt = Okt()

tokens = okt.morphs("만약 우리가 함께 할 수 없는 내일이 있다면 한 가지 네가 언제나 기억할 것이 있어. 넌 네가 믿고 있는 것보다 더 용감하고, 보기보다 더 강하고, 네 생각보다 더 똑똑해.")

print(tokens)

#['만약', '우리', '가', '함께', '할', '수', '없는', '내일', '이', '있다면', '한', '가지', '네', '가', '언제나', '기억', '할', '것', '이', '있어', '.', '넌', '네', '가', '믿고', '있는', '것', '보다', '더', '용감하고', ',', '보기', '보다', '더', '강하고', ',', '네', '생각', '보다', '더', '똑똑해', '.']

  

word_to_index = {word : index for index, word in enumerate(tokens)}

print('단어 집합 :', word_to_index)

#단어 집합 : {'만약': 0, '우리': 1, '가': 23, '함께': 3, '할': 16, '수': 5, '없는': 6, '내일': 7, '이': 18, '있다면': 9, '한': 10, '가지': 11, '네': 36, '언제나': 14, '기억': 15, '것': 26, '있어': 19, '.': 41, '넌': 21, '믿고': 24, '있는': 25, '보다': 38, '더': 39, '용감하고': 29, ',': 35, '보기': 31, '강하고': 34, '생각': 37, '똑똑해': 40}

  

def one_hot_encoding(word, word_to_index):

one_hot_vector = [0]*(len(word_to_index))

index = word_to_index[word]

one_hot_vector[index] = 1

return one_hot_vector

  

print(one_hot_encoding("것", word_to_index))

#[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0]

  
  

#One-Hot Encoding with keras

  

from tensorflow.keras.preprocessing.text import Tokenizer

from tensorflow.keras.utils import to_categorical

  

story = "우리는 추억을 만든다고 생각하지 않았어. 우리는 단지 재미있게 지냈을 뿐이야."

  

tokenizer = Tokenizer()

tokenizer.fit_on_texts([story])

print('Story :', tokenizer.word_index)

#Story : {'우리는': 1, '추억을': 2, '만든다고': 3, '생각하지': 4, '않았어': 5, '단지': 6, '재미있게': 7, '지냈을': 8, '뿐이야': 9}

  

sub_story = "추억을 만든다고 생각하지 않았어. 단지 재미있게 지냈을 뿐이야."

encoded = tokenizer.texts_to_sequences([sub_story])[0]

print(encoded)

#[2, 3, 4, 5, 6, 7, 8, 9]

  

one_hot = to_categorical(encoded)

print(one_hot)

'''

[[0. 0. 1. 0. 0. 0. 0. 0. 0. 0.]

[0. 0. 0. 1. 0. 0. 0. 0. 0. 0.]

[0. 0. 0. 0. 1. 0. 0. 0. 0. 0.]

[0. 0. 0. 0. 0. 1. 0. 0. 0. 0.]

[0. 0. 0. 0. 0. 0. 1. 0. 0. 0.]

[0. 0. 0. 0. 0. 0. 0. 1. 0. 0.]

[0. 0. 0. 0. 0. 0. 0. 0. 1. 0.]

[0. 0. 0. 0. 0. 0. 0. 0. 0. 1.]]

'''
```