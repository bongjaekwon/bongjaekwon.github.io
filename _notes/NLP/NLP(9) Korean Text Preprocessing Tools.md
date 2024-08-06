---
title: NLP(9) Korean Text Preprocessing Tools
feed: show
date: 05-08-2024
---
#### Posting information

- Posting Date : 05-08-2024  
- Last Edit : 05-08-2024  
- Writer : KWON Bongjae

#### Posting detail

```
#01_09 Korean Text Preprocessing Tools

  

#spcing with pykospacing

  

story = '다행히 비는 오지 않았습니다. 크리스토퍼 로빈은 나무 조각들을 모아 긴 테이블을 만들었고, 친구들 모두 테이블 주위에 앉았습니다. 크리스토퍼 로빈은 한쪽 끝에 앉았고, 푸는 다른 쪽 끝에 앉았고, 두 친구 사이에 부엉이와 이요르와 피글렛이, 그리고 그 반대편에는 래빗과 루와 캉가가 있었습니다. 그리고 래빗의 모든 친구들과 친척들은 잔디 위에 누워 누군가가 그들에게 말을 걸거나 그들 근처에 무엇인가를 떨어뜨리거나 시간을 물어보기를 바랐습니다.'

  

story_without_space = story.replace(" ", '')

print(story_without_space)

#다행히비는오지않았습니다.크리스토퍼로빈은나무조각들을모아긴테이블을만들었고,친구들모두테이블주위에앉았습니다.크리스토퍼로빈은한쪽끝에앉았고,푸는다른쪽끝에앉았고,두친구사이에부엉이와이요르와피글렛이,그리고그반대편에는래빗과루와캉가가있었습니다.그리고래빗의모든친구들과친척들은잔디위에누워누군가가그들에게말을걸거나그들근처에무엇인가를떨어뜨리거나시간을물어보기를바랐습니다.

  

from pykospacing import Spacing

spacing = Spacing()

kospacing_story = spacing(story_without_space)

  

print(kospacing_story)

#다행히 비는 오지 않았습니다. 크리스토퍼로 빈은 나무 조각들을 모아 긴 테이블을 만들었고, 친구들 모두 테이블 주위에 앉았습니다. 크리스토퍼로 빈은 한쪽 끝에 앉았고, 푸는 다른 쪽 끝에 앉았고, 두 친구 사이에 부엉이와 이 요르와 피글렛이, 그리고 그 반대편에는 래빗과 루와 캉가가 있었습니다. 그리고 래빗의 모든 친구들과 친척들은 잔디 위에 누워 누군가가 그들에게 말을 걸거나 그들 근처에 무엇인가를 떨어뜨리거나 시간을 물어보기를 바랐습니다.

#spacing well!

  
  

#tokenization using SOYNLP

  

from konlpy.tag import Okt

tokenizer = Okt()

print(tokenizer.morphs('러브라이브 최애캐 당연히 소노다우미 우미쨩 다이스키 선샤인 인정노노'))

#['러브라이브', '최애캐', '당연히', '소', '노', '다', '우미', '우미', '쨩', '다이스', '키', '선샤인', '인정', '노노']

  

import urllib.request

from soynlp import DoublespaceLineCorpus

from soynlp.word import WordExtractor

  

f = open("/home/kwon/Desktop/In Work/개인/Winnie the Pooh.txt", 'r')

while True:

line = f.readline()

if not line : break

f.close()

  

corpus = DoublespaceLineCorpus("/home/kwon/Desktop/In Work/개인/Winnie the Pooh.txt")

print(len(corpus))

#4010

  

i = 0

for doc in corpus:

if len(doc) > 0:

print(doc)

i = i +1

if i == 20:

break

  

'''

The Project Gutenberg eBook of Winnie-the-Pooh

This ebook is for the use of anyone anywhere in the United States and

most other parts of the world at no cost and with almost no restrictions

whatsoever. You may copy it, give it away or re-use it under the terms

of the Project Gutenberg License included with this ebook or online

at www.gutenberg.org. If you are not located in the United States,

you will have to check the laws of the country where you are located

before using this eBook.

Title: Winnie-the-Pooh

Author: A. A. Milne

Illustrator: Ernest H. Shepard

Release date: January 3, 2022 [eBook #67098]

Most recently updated: December 28, 2022

Language: English

Original publication: Canada: McClelland & Stewart, Ltd, 1926

Credits: Greg Weeks, Mary Meehan, Iona Vaughan, David T. Jones and the online Distributed Proofreaders Canada team at http://www.pgdpcanada.net

*** START OF THE PROJECT GUTENBERG EBOOK WINNIE-THE-POOH ***

WINNIE-THE-POOH

_BY A. A. MILNE_

_JUVENILES_

'''

  

word_extractor = WordExtractor()

word_extractor.train(corpus)

word_score_table = word_extractor.extract()

'''

training was done. used memory 0.968 Gbry 0.959 Gb

all cohesion probabilities was computed. # words = 4386

all branching entropies was computed # words = 6340

all accessor variety was computed # words = 6340

'''



print(word_score_table["Winnie"].cohesion_forward)

#0.7464617656990232

  

print(word_score_table["Po"].cohesion_forward)

#0.5

  

print(word_score_table["Poo"].cohesion_forward)

#0.680448531544916

  

print(word_score_table["Pooh"].cohesion_forward)

#0.7707723533036147
```

### cohesion probability

![](https://lh3.googleusercontent.com/pw/AP1GczP25TutcQ_Vs49XAOx1zX-f_0weIb7La4ICP5aO_GIsXzqahcwPiuyrlys5vsVyN_grf7pHvRsuOqt6QFJYB7jIoMgGSFJPrG0IUiwyd-waT3BY4JP30DF4JcElmJuyEMErgsoVg6IP49OwfZ6ch0uU9g=w744-h84-s-no?authuser=0)

This formula is used to measure the cohesion in a text, such as the lexical cohesion within a sequence. Here’s how it can be understood:

1. **Part**
	1. ∏ part : The product symbol. This represents the product over i from 1 to n−1
	2. probability part : The conditional probability occurring given the sequence
	3. c1:i+1 \| c1:i part : The subsequence from the first element to the i-th element of the text.
	4. root part : Takes the (n−1)th root of the product
	
2.  **Steps of Calculation**
	1. Calculate Conditional Probabilities
		- For each word ci+1​, calculate the probability of it occurring given the preceding sequence c1:i
	2. Multiplication
		- Multiply all these conditional probabilities from the first pair of words to the last pair.
	3. Normalization
		- Take the root of the entire product. Since there are n−1 pairs of words, this is effectively calculating the geometric mean
	
3. **Example**
	- Consider a text sequence "곰 돌 이 푸",
		- c1 = "곰"
		- c2 = "돌"
		- c3 = "이"
		- c4 = "푸"
	- The conditional probabilities are 
		- P(c2 \| c1) : Probability of "돌" occurring given "곰"
		- P(c3 \| c1c2) : Probability of "이" occurring given "곰 돌"
		- P(c4 \| c1c2c3) : Probability of "푸" occurring given "곰 돌 이"
	- Apply the cohesion formula,
		- Calculate the product of these conditional probabilities:
![](https://lh3.googleusercontent.com/pw/AP1GczPK4DZqqm2pgsXK-v3n8r6eTYgF2XjDl0yAXUKv8DyfBbBIKjkqwFazkcwavblmQQtdR6vbfxIQJS4WujpOcKnNdpnALilsTSLhsNn6hYnKVxhMP9ZPYuvRVQlOypsOKxZXSgJAh3DaKZGVeVZXnehM_w=w730-h40-s-no?authuser=0)
		- The geometric mean of the product:
![](https://lh3.googleusercontent.com/pw/AP1GczPXBVTFLjE-zihEMc_OkmFSZ_ZxoCAz1npZwn8W8PPRcK60hf5GhGetGEq4iUuwU732FpxxDcKU8Wf0DpehV1eTVZZ0R_yOCT_UW8FjwrGVSx6AExqsbDsrItSMLJwdzJ-dUnkDYxzvcfdgfby2SCE7WQ=w730-h40-s-no?authuser=0)
	- Example calculation(Example probabilities)
		- Assume the following conditional probabilities for the sake of example:
			- P(돌 \| 곰) = 0.4
			- P(이 \| 곰 돌) = 0.5
			- P(푸 \| 곰 돌 이) = 0.6
		- Apply these to the formula:
![](https://lh3.googleusercontent.com/pw/AP1GczMrvx_38n4bh1bbyLieQuU7Mt1idK3KoGA3hAFh9cfLgPqeFPWIv8NFHb58yrQe-XSy8JOFo6lE-yXo13BAB9b210N7WDmtG35OaDDXqxAgkrD8MMI9MuNhFfl9UxdaYSEeG3QJQkwCfwSLS8hv3s0XXA=w730-h102-s-no?authuser=0)		Therefore, the cohesion of the sequence "곰 돌 이 푸" whit this given probabilities is approximately 0.494.

4. **Example2**

```
f = open("/home/kwon/Desktop/In Work/개인/염쟁이유씨.txt", 'r')

while True:

line = f.readline()

if not line : break

f.close()

  

corpus = DoublespaceLineCorpus("/home/kwon/Desktop/In Work/개인/염쟁이유씨.txt")

print(len(corpus))

#679

  

i = 0

for doc in corpus:

if len(doc) > 0:

print(doc)

i = i +1

if i == 20:

break

'''

염쟁이 유氏

(연극쟁이 유순웅을 위한 일인극)

김 인 경

곳곳에는 관, 종이꽃,완성 되지 않은 꽃상여, 곱게 접혀 있는 수의, 각종 크기의 삼베천, 칠성판,

짚세기, 향로, 병풍 등 장례식에 쓰임직한 갖가지 것들이 차곡차곡 쌓여있거나 혹은 무질서하게

널부러져 있다.

마당 한 켠에는 흰 천에 덮인 시신이 한 구 놓여있다.

유씨 : (핸드폰 안테나를 최대한 뽑아 올린 채, 이리저리 방향을 맞춰보며 짜증이 나있는

표정으로 나온다) 제기랄! 이게 왜 안터지냐구. 꼭 밖으로 나가야 통 화가 되니, 전화 올 때마다

성가셔서 살수가 있나.

(관객들에게) 거 핸드폰 있는 사람 나한테 전화 좀 날려보셔. 0-1-7-4-3- (핸드폰을

꺼내는 관객이 있으면) 어허! 이거봐, 이거보라구..내 이럴 줄 알 았다니까.

이런 자리에 오면 제일 먼저 해야하는 일이 핸드폰 죽이는 거라는 건 이제 일반상식

아녀? 얼른들 꺼! 진동도 안되야! 게다가 지금 이 자리가 예삿 자 리여? 죽은 사람 염하는 자리여.

염이 뭐여. 관으로 들어가기 직전의 장의 절차아녀? 그러니까 저기 놓여있는 게 바로 시신이지.

시체! 왜 겁나냐?

죽은 사람이 무섭긴 뭐가 무서워, 산 사람이 더 무섭지. 송장이 사기 치는거 봤어?

송장이 사람 죽이는 거 봤냐구. 죽은 사람이 산 사람 헤꼬지 하는 법 없으니까 걱정들 꽉 붙들어

매셔. 내가 왜 이리 자신만만하냐구? 내가 한 평생 해온 일이 바로 그거거든. 염쟁이! 그게 내

밥줄여. 죽은 사람이 날 먹 여 살려. 말하기 좋아허는 놈들이 그러대. 사람이 죽어야 유씨가 살지.

'''

  

word_extractor = WordExtractor()

word_extractor.train(corpus)

word_score_table = word_extractor.extract()

'''

training was done. used memory 0.984 Gby 0.981 Gb

all cohesion probabilities was computed. # words = 569

all branching entropies was computed # words = 1279

all accessor variety was computed # words = 1279

'''

  

print(word_score_table["염쟁"].cohesion_forward)

#0.208955223880597

  

print(word_score_table["염쟁이"].cohesion_forward)

#0.45711620391383745
```
