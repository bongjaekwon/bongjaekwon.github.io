---
title: NLP_Tokenization
feed: show
date: 01-08-2024
---
Article, Keyword, Publisher

#### Posting information

- Posting Date : 01-08-2024  
- Last Edit : 01-08-2024  
- Writer : KWON Bongjae

#### Posting detail

```
#01_01 : Tokenization

  

#_01_01_01 : Word Tokenization

from nltk.tokenize import word_tokenize

from nltk.tokenize import WordPunctTokenizer

from tensorflow.keras.preprocessing.text import text_to_word_sequence

  

#print('word tokenization 1 :',word_tokenize("Here's Edward Bear, coming downstairs now, bump, bump, bump, on the back of his head, behind Christopher Robin."))

  

#word tokenization 1 : ['Here', "'s", 'Edward', 'Bear', ',', 'coming', 'downstairs', 'now', ',', 'bump', ',', 'bump', ',', 'bump', ',', 'on', 'the', 'back', 'of', 'his', 'head', ',', 'behind', 'Christopher', 'Robin', '.']

  
  

#print('word tokenization 2 :',WordPunctTokenizer().tokenize("Here's Edward Bear, coming downstairs now, bump, bump, bump, on the back of his head, behind Christopher Robin."))

  

#word tokenization 2 : ['Here', "'", 's', 'Edward', 'Bear', ',', 'coming', 'downstairs', 'now', ',', 'bump', ',', 'bump', ',', 'bump', ',', 'on', 'the', 'back', 'of', 'his', 'head', ',', 'behind', 'Christopher', 'Robin', '.']

  
  

#print('word tokenization 3 :',text_to_word_sequence("Here's Edward Bear, coming downstairs now, bump, bump, bump, on the back of his head, behind Christopher Robin."))

  

#word tokenization 3 : ["here's", 'edward', 'bear', 'coming', 'downstairs', 'now', 'bump', 'bump', 'bump', 'on', 'the', 'back', 'of', 'his', 'head', 'behind', 'christopher', 'robin']

  
  

#_01_01_02 : Tokenizing Standard

  

#Penn Treebank Tokenization

#Rule 1. Keep a word consisting of a hypoon as one.

#Rule 2. Separate words with apostrophe 'folding', such as doesn't.

  

from nltk.tokenize import TreebankWordTokenizer

  

tokenizer = TreebankWordTokenizer()

  

#text = "Winnie-the-Pooh sat down at the foot of the tree, put his head between his paws and began to think."

#print('Treebank Word Tokenizer :',tokenizer.tokenize(text))

  

#Treebank Word Tokenizer : ['Winnie-the-Pooh', 'sat', 'down', 'at', 'the', 'foot', 'of', 'the', 'tree', ',', 'put', 'his', 'head', 'between', 'his', 'paws', 'and', 'began', 'to', 'think', '.']

  
  

#_01_01_03 : Sentence Tokenization

  

from nltk.tokenize import sent_tokenize

  

#text = "And Piglet wished very much that his Grandfather T. W. were there, instead of elsewhere, and Pooh thought how nice it would be if they met Christopher Robin suddenly but quite accidentally, and only because he liked Christopher Robin so much. And then, all of a sudden, Winnie-the-Pooh stopped again, and licked the tip of his nose in a cooling manner, for he was feeling more hot and anxious than ever in his life before."

#print('sent_tokenize 1 :',sent_tokenize(text))

  

#sent_tokenize 1 : ['And Piglet wished very much that his Grandfather T. W. were there, instead of elsewhere, and Pooh thought how nice it would be if they met Christopher Robin suddenly but quite accidentally, and only because he liked Christopher Robin so much.', 'And then, all of a sudden, Winnie-the-Pooh stopped again, and licked the tip of his nose in a cooling manner, for he was feeling more hot and anxious than ever in his life before.']

  

import kss

  

#text = '곰돌이 푸우는 두 장의 안내문을 아주 조심스럽게, 왼쪽부터 읽기 시작했습니다. 행여 놓친 부분이 있을 것을 대비해서 오른쪽부터 또다시 읽었지요. 그런 다음 노크를 하고 문을 열었습니다. 올빼미를 부르기 위해서요.'

#print('한국어 문장 토큰화 :',kss.split_sentences(text))

  

#한국어 문장 토큰화 : ['곰돌이 푸우는 두 장의 안내문을 아주 조심스럽게, 왼쪽부터 읽기 시작했습니다.', '행여 놓친 부분이 있을 것을 대비해서 오른쪽부터 또다시 읽었지요.', '그런 다음 노크를 하고 문을 열었습니다.', '올빼미를 부르기 위해서요.']

  
  

#_01_01_04 : Part-of-speech tagging

  

from nltk.tokenize import word_tokenize

from nltk.tag import pos_tag

  

#text = "Winnie-the-Pooh sat down at the foot of the tree, put his head between his paws and began to think."

#tokenized_sentence = word_tokenize(text)

#print('Part-of-speech tagging :',pos_tag(tokenized_sentence))

  

#Part-of-speech tagging : [('Winnie-the-Pooh', 'JJ'), ('sat', 'VBD'), ('down', 'RB'), ('at', 'IN'), ('the', 'DT'), ('foot', 'NN'), ('of', 'IN'), ('the', 'DT'), ('tree', 'NN'), (',', ','), ('put', 'VBD'), ('his', 'PRP$'), ('head', 'NN'), ('between', 'IN'), ('his', 'PRP$'), ('paws', 'NN'), ('and', 'CC'), ('began', 'VBD'), ('to', 'TO'), ('think', 'VB'), ('.', '.')]

#Part of speech tagging was performed by inputting the result of tokenization for English sentences. In Penn Trebank POG Tags, PRP is a personal pronoun, VBP is a verb, RB is an adverb, VBG is a present adverb, IN is a preposition, NNP is a proper noun, NNS is a plural noun, JJ is is a adjective, CC is a conjunction, and DT is an official.

  
  

from konlpy.tag import Okt

from konlpy.tag import Kkma

  

okt = Okt()

kkma = Kkma()

  

#print('OKT 형태소 분석 :',okt.morphs("곰돌이 푸우는 두 장의 안내문을 아주 조심스럽게, 왼쪽부터 읽기 시작했습니다"))

#print('OKT 품사 태깅 :',okt.pos("곰돌이 푸우는 두 장의 안내문을 아주 조심스럽게, 왼쪽부터 읽기 시작했습니다"))

#print('OKT 명사 추출 :',okt.nouns("곰돌이 푸우는 두 장의 안내문을 아주 조심스럽게, 왼쪽부터 읽기 시작했습니다"))

#OKT 형태소 분석 : ['곰돌이', '푸우', '는', '두', '장의', '안', '내', '문을', '아주', '조심', '스럽게', ',', '왼쪽', '부터', '읽기', '시작', '했습니다']

#OKT 품사 태깅 : [('곰돌이', 'Noun'), ('푸우', 'Noun'), ('는', 'Josa'), ('두', 'Noun'), ('장의', 'Noun'), ('안', 'VerbPrefix'), ('내', 'VerbPrefix'), ('문을', 'Verb'), ('아주', 'Noun'), ('조심', 'Noun'), ('스럽게', 'Josa'), (',', 'Punctuation'), ('왼쪽', 'Noun'), ('부터', 'Josa'), ('읽기', 'Verb'), ('시작', 'Noun'), ('했습니다', 'Verb')]

#OKT 명사 추출 : ['곰돌이', '푸우', '두', '장의', '아주', '조심', '왼쪽', '시작']

  

#print('꼬꼬마 형태소 분석 :',kkma.morphs("곰돌이 푸우는 두 장의 안내문을 아주 조심스럽게, 왼쪽부터 읽기 시작했습니다"))

#print('꼬꼬마 품사 태깅 :',kkma.pos("곰돌이 푸우는 두 장의 안내문을 아주 조심스럽게, 왼쪽부터 읽기 시작했습니다"))

#print('꼬꼬마 명사 추출 :',kkma.nouns("곰돌이 푸우는 두 장의 안내문을 아주 조심스럽게, 왼쪽부터 읽기 시작했습니다"))

#꼬꼬마 형태소 분석 : ['곰돌이', '푸우', '는', '두', '장의', '안내문', '을', '아주', '조심', '스럽', '게', ',', '왼쪽', '부터', '읽기', '시작하', '었', '습니다']

#꼬꼬마 품사 태깅 : [('곰돌이', 'NNG'), ('푸우', 'MAG'), ('는', 'JX'), ('두', 'MDN'), ('장의', 'NNG'), ('안내문', 'NNG'), ('을', 'JKO'), ('아주', 'MAG'), ('조심', 'NNG'), ('스럽', 'XSA'), ('게', 'ECD'), (',', 'SP'), ('왼쪽', 'NNG'), ('부터', 'JX'), ('읽기', 'NNG'), ('시작하', 'VV'), ('었', 'EPT'), ('습니다', 'EFN')]

#꼬꼬마 명사 추출 : ['곰돌이', '장의', '안내문', '조심', '왼쪽', '읽기']
```