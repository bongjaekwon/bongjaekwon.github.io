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

  

urllib.request.urlretrieve("https://raw.githubusercontent.com/lovit/soynlp/master/tutorials/2016-10-20.txt", filename="2016-10-20.txt")

  

corpus = DoublespaceLineCorpus("2016-10-20.txt")

print(len(corpus))

#30091

  

i = 0

for doc in corpus:

if len(doc) > 0:

print(doc)

i = i +1

if i == 5:

break

  

'''

19 1990 52 1 22

오패산터널 총격전 용의자 검거 서울 연합뉴스 경찰 관계자들이 19일 오후 서울 강북구 오패산 터널 인근에서 사제 총기를 발사해 경찰을 살해한 용의자 성모씨를 검거하고 있다 성씨는 검거 당시 서바이벌 게임에서 쓰는 방탄조끼에 헬멧까지 착용한 상태였다 독자제공 영상 캡처 연합뉴스 서울 연합뉴스 김은경 기자 사제 총기로 경찰을 살해한 범인 성모 46 씨는 주도면밀했다 경찰에 따르면 성씨는 19일 오후 강북경찰서 인근 부동산 업소 밖에서 부동산업자 이모 67 씨가 나오기를 기다렸다 이씨와는 평소에도 말다툼을 자주 한 것으로 알려졌다 이씨가 나와 걷기 시작하자 성씨는 따라가면서 미리 준비해온 사제 총기를 이씨에게 발사했다 총알이 빗나가면서 이씨는 도망갔다 그 빗나간 총알은 지나가던 행인 71 씨의 배를 스쳤다 성씨는 강북서 인근 치킨집까지 이씨 뒤를 쫓으며 실랑이하다 쓰러뜨린 후 총기와 함께 가져온 망치로 이씨 머리를 때렸다 이 과정에서 오후 6시 20분께 강북구 번동 길 위에서 사람들이 싸우고 있다 총소리가 났다 는 등의 신고가 여러건 들어왔다 5분 후에 성씨의 전자발찌가 훼손됐다는 신고가 보호관찰소 시스템을 통해 들어왔다 성범죄자로 전자발찌를 차고 있던 성씨는 부엌칼로 직접 자신의 발찌를 끊었다 용의자 소지 사제총기 2정 서울 연합뉴스 임헌정 기자 서울 시내에서 폭행 용의자가 현장 조사를 벌이던 경찰관에게 사제총기를 발사해 경찰관이 숨졌다 19일 오후 6시28분 강북구 번동에서 둔기로 맞았다 는 폭행 피해 신고가 접수돼 현장에서 조사하던 강북경찰서 번동파출소 소속 김모 54 경위가 폭행 용의자 성모 45 씨가 쏜 사제총기에 맞고 쓰러진 뒤 병원에 옮겨졌으나 숨졌다 사진은 용의자가 소지한 사제총기 신고를 받고 번동파출소에서 김창호 54 경위 등 경찰들이 오후 6시 29분께 현장으로 출동했다 성씨는 그사이 부동산 앞에 놓아뒀던 가방을 챙겨 오패산 쪽으로 도망간 후였다 김 경위는 오패산 터널 입구 오른쪽의 급경사에서 성씨에게 접근하다가 오후 6시 33분께 풀숲에 숨은 성씨가 허공에 난사한 10여발의 총알 중 일부를 왼쪽 어깨 뒷부분에 맞고 쓰러졌다 김 경위는 구급차가 도착했을 때 이미 의식이 없었고 심폐소생술을 하며 병원으로 옮겨졌으나 총알이 폐를 훼손해 오후 7시 40분께 사망했다 김 경위는 외근용 조끼를 입고 있었으나 총알을 막기에는 역부족이었다 머리에 부상을 입은 이씨도 함께 병원으로 이송됐으나 생명에는 지장이 없는 것으로 알려졌다 성씨는 오패산 터널 밑쪽 숲에서 오후 6시 45분께 잡혔다 총격현장 수색하는 경찰들 서울 연합뉴스 이효석 기자 19일 오후 서울 강북구 오패산 터널 인근에서 경찰들이 폭행 용의자가 사제총기를 발사해 경찰관이 사망한 사건을 조사 하고 있다 총 때문에 쫓던 경관들과 민간인들이 몸을 숨겼는데 인근 신발가게 직원 이모씨가 다가가 성씨를 덮쳤고 이어 현장에 있던 다른 상인들과 경찰이 가세해 체포했다 성씨는 경찰에 붙잡힌 직후 나 자살하려고 한 거다 맞아 죽어도 괜찮다 고 말한 것으로 전해졌다 성씨 자신도 경찰이 발사한 공포탄 1발 실탄 3발 중 실탄 1발을 배에 맞았으나 방탄조끼를 입은 상태여서 부상하지는 않았다 경찰은 인근을 수색해 성씨가 만든 사제총 16정과 칼 7개를 압수했다 실제 폭발할지는 알 수 없는 요구르트병에 무언가를 채워두고 심지를 꽂은 사제 폭탄도 발견됐다 일부는 숲에서 발견됐고 일부는 성씨가 소지한 가방 안에 있었다

테헤란 연합뉴스 강훈상 특파원 이용 승객수 기준 세계 최대 공항인 아랍에미리트 두바이국제공항은 19일 현지시간 이 공항을 이륙하는 모든 항공기의 탑승객은 삼성전자의 갤럭시노트7을 휴대하면 안 된다고 밝혔다 두바이국제공항은 여러 항공 관련 기구의 권고에 따라 안전성에 우려가 있는 스마트폰 갤럭시노트7을 휴대하고 비행기를 타면 안 된다 며 탑승 전 검색 중 발견되면 압수할 계획 이라고 발표했다 공항 측은 갤럭시노트7의 배터리가 폭발 우려가 제기된 만큼 이 제품을 갖고 공항 안으로 들어오지 말라고 이용객에 당부했다 이런 조치는 두바이국제공항 뿐 아니라 신공항인 두바이월드센터에도 적용된다 배터리 폭발문제로 회수된 갤럭시노트7 연합뉴스자료사진

브뤼셀 연합뉴스 김병수 특파원 독일 정부는 19일 원자력발전소를 폐쇄하기로 함에 따라 원자력 발전소 운영자들에게 핵폐기물 처리를 지원하는 펀드에 235억 유로 260억 달러 29조 원 를 지불하도록 하는 계획을 승인했다고 언론들이 보도했다 앞서 독일은 5년 전 일본 후쿠시마 원전사태 이후 오는 2022년까지 원전 17기를 모두 폐쇄하기로 하고 오는 2050년까지 전기생산량의 80 를 재생에너지로 충당하는 것을 목표로 세웠다 이날 내각을 통과한 법안은 원전 운영자들이 원전 해체와 핵폐기물 처리를 위한 포장을 책임지고 정부는 핵폐기물 보관을 책임지도록 했다 독일 경제부는 전력회사들과 공식적인 접촉은 아직 합의되지 않았다고 밝혔다 독일 원자력 발전소 연합뉴스 자료사진

서울 연합뉴스 19일 서울 강북구에서 사제 총기범이 쏜 총탄에 숨진 김창호 54 경위의 생전 모습 김 경위는 의협심 강하고 솔선수범하는 참된 경찰관이었다는 평가를 받는다 2016 10 20 서울 강북경찰서 제공 연합뉴스

'''

  

word_extractor = WordExtractor()

word_extractor.train(corpus)

word_score_table = word_extractor.extract()

'''

training was done. used memory 1.604 Gb

all cohesion probabilities was computed. # words = 223348

all branching entropies was computed # words = 361598

all accessor variety was computed # words = 361598

'''
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