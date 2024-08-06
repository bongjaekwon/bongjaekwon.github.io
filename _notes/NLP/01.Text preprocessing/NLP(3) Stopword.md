---
title: NLP(3) Stopword
feed: show
date: 02-08-2024
---
#### Posting information

- Posting Date : 02-08-2024  
- Last Edit : 02-08-2024  
- Writer : KWON Bongjae

#### Posting detail

```
#01_03 : Stopword

from nltk.corpus import stopwords

from nltk.tokenize import word_tokenize

from konlpy.tag import Okt

  

#_01_02_01 : Stopwords in NLTK

  

#stop_words_list = stopwords.words('english')

#print('Count stopwords :', len(stop_words_list))

#print('print 28 :',stop_words_list[:28])

#print 28 : ['i', 'me', 'my', 'myself', 'we', 'our', 'ours', 'ourselves', 'you', "you're", "you've", "you'll", "you'd", 'your', 'yours', 'yourself', 'yourselves', 'he', 'him', 'his', 'himself', 'she', "she's", 'her', 'hers', 'herself', 'it', "it's"]

  
  

#_01_02_02 : Eleminating stopwords in NLTK

  

example = """

So with these words he unhooked it, and carried it back to Eeyore; and when Christopher Robin had nailed it on in its right place again, Eeyore frisked about the forest, waving his tail so happily that Winnie-the-Pooh came over all funny, and had to hurry home for a little snack of something to sustain him.

"""

stop_words = set(stopwords.words('english'))

  

word_tokens = word_tokenize(example)

  

result = []

for word in word_tokens:

if word not in stop_words:

result.append(word)

  

print('Befpre :',word_tokens)

print('After :',result)

  

#Befpre : ['So', 'with', 'these', 'words', 'he', 'unhooked', 'it', ',', 'and', 'carried', 'it', 'back', 'to', 'Eeyore', ';', 'and', 'when', 'Christopher', 'Robin', 'had', 'nailed', 'it', 'on', 'in', 'its', 'right', 'place', 'again', ',', 'Eeyore', 'frisked', 'about', 'the', 'forest', ',', 'waving', 'his', 'tail', 'so', 'happily', 'that', 'Winnie-the-Pooh', 'came', 'over', 'all', 'funny', ',', 'and', 'had', 'to', 'hurry', 'home', 'for', 'a', 'little', 'snack', 'of', 'something', 'to', 'sustain', 'him', '.']

  

#After : ['So', 'words', 'unhooked', ',', 'carried', 'back', 'Eeyore', ';', 'Christopher', 'Robin', 'nailed', 'right', 'place', ',', 'Eeyore', 'frisked', 'forest', ',', 'waving', 'tail', 'happily', 'Winnie-the-Pooh', 'came', 'funny', ',', 'hurry', 'home', 'little', 'snack', 'something', 'sustain', '.']

  
  
  

#_01_02_02 : Eleminating stopwords in Korean

  

okt = Okt()

  

example = """

그리고 나서 친구들은 각자 이야기 거리를 꺼내 대화를 나누었습니다. 푸와 피글렛이 함께 집으로 돌아갈 시간이 될 때까지 말입니다. 그들은 백 에이커 너머에 있는 나무의 가장자리에 있는 길을 더듬어 가면서 서로에게 많은 말을 하지 않았습니다

"""

stop_words = "나서 각자 함께 될 너머에 있는"

  

stop_words = set(stop_words.split(' '))

word_tokens = okt.morphs(example)

  

result = [word for word in word_tokens if not word in stop_words]

  

print('불용어 제거 전 :',word_tokens)

print('불용어 제거 후 :',result)

#불용어 제거 전 : ['\n', '그리고', '나서', '친구', '들', '은', '각자', '이야기', '거리', '를', '꺼내', '대화', '를', '나누었습니다', '.', '푸와', '피글렛', '이', '함께', '집', '으로', '돌아갈', '시간', '이', '될', '때', '까지', '말', '입니다', '.', '그', '들', '은', '백', '에이커', '너머', '에', '있는', '나무', '의', '가장자리', '에', '있는', '길', '을', '더듬어', '가면', '서', '서로', '에게', '많은', '말', '을', '하지', '않았습니다', '\n']

#불용어 제거 후 : ['\n', '그리고', '친구', '들', '은', '이야기', '거리', '를', '꺼내', '대화', '를', '나누었습니다', '.', '푸와', '피글렛', '이', '집', '으로', '돌아갈', '시간', '이', '때', '까지', '말', '입니다', '.', '그', '들', '은', '백', '에이커', '너머', '에', '나무', '의', '가장자리', '에', '길', '을', '더듬어', '가면', '서', '서로', '에게', '많은', '말', '을', '하지', '않았습니다', '\n']
```