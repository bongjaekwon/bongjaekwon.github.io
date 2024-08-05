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

  

urllib.request.urlretrieve()
```