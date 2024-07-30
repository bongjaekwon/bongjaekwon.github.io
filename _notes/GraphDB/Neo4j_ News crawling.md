---
title: Neo4j_ News crawling
feed: show
date: 30-07-2024
---
Article, Keyword, Publisher

#### Posting information

- Posting Date : 30-07-2024  
- Last Edit : 30-07-2024  
- Writer : KWON Bongjae

#### Environment information

- Hardware : MacBookPro8,2(late 11) /  8 × Intel® Core™ i7-2675QM CPU @ 2.20GHz / RAM 15.5 GiB / Mesa Intel® HD Graphics 3000 <br>
- OS : Linux(openSUSE Tumbleweed 20240716) <br>
- DB : ArcadeDB, Neo4j Community 5.21.2 (using Cypher / openCypher) <br> 
#### Posting detail

![](https://lh3.googleusercontent.com/pw/AP1GczOA5m8MIfZ6ffzWGMGUGh6isEj6ASUR5Iwz6jI_f7gJWBQt8Zkq-1c7L27qqnTQpIUS-B5wGnbDUIZkJfJUUhkxhcbVeASiH0E2Tc_7mU2pIP2ninR4KrCGF7RNVJFYopFA9_67XySDLYabo8L3iXM0Cw=w1440-h780-s-no?authuser=0)

![](https://lh3.googleusercontent.com/pw/AP1GczNfhZzCD5Px06mjDVqWgr_jG8Iu7dnHUMnwpHY1Ps99iZI4cENI_ZDPr6LhV9JG90k2sinUiSHApTzDM64vwtI6WZzPa6AfBn7TlFwNhikp6ycBgqME-nA5-5wOgk4W4dU8nfL607gvifDdSbez9BBvfw=w1440-h781-s-no?authuser=0)


- News crawling

```
import requests
from bs4 import BeautifulSoup as BS
import pandas as pd
import numpy as np
import re

headers = {'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.135 Safari/537.36'}

d_list = []
start_data = 20240725
end_data = 20240730
for date_int in range(start_data, end_data):
date = str(date_int)
url = "https://news.naver.com/main/ranking/popularDay.nhn?date=" + date
html = requests.get(url, headers=headers).text
soup = BS(html, 'html.parser')
ranking_total = soup.find_all(class_='rankingnews_box')

for item in ranking_total:
media = item.a.strong.text
news = item.find_all(class_="list_content")
for new in news:
d = {}
d['media'] = media
d['src'] = "https://news.naver.com/" + new.a['href']
d['title'] = new.a.text
d['date'] = date
d_list.append(d)
df = pd.DataFrame(d_list)

def clean_text(row):
text = row['title']
pattern = '([a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+)'
text = re.sub(pattern=pattern, repl='', string=text)
pattern = '(http|ftp|https)://(?:[-\w.]|(?:%[\da-fA-F]{2}))+'
text = re.sub(pattern=pattern, repl='', string=text)
pattern = '([ㄱ-ㅎㅏ-ㅣ]+)'
text = re.sub(pattern=pattern, repl='', string=text)
pattern = '<[^>]*>'
text = re.sub(pattern=pattern, repl='', string=text)
pattern = r'\([^)]*\)'
text = re.sub(pattern=pattern, repl='', string=text)
pattern = '[^\w\s]'
text = re.sub(pattern=pattern, repl='', string=text)
pattern = '[^\w\s]'
text = re.sub(pattern=pattern, repl='', string=text)
pattern = '["단독"]'
text = re.sub(pattern=pattern, repl='', string=text)
pattern = '["속보"]'
text = re.sub(pattern=pattern, repl='', string=text)
text = text.strip()
text = " ".join(text.split())
return text

df['title_c'] = df.apply(clean_text, axis=1)

from konlpy.tag import Kkma
from konlpy.tag import Komoran
kkma = Kkma()
komoran = Komoran()

df['keyword'] = ''
for idx_line in range(len(df)):
nouns_list = komoran.nouns(df['title_c'].loc[idx_line])
nouns_list_c = [nouns for nouns in nouns_list if len(nouns) > 1] # 한글자는 이상한게 많아서 2글자 이상
df.at[idx_line, 'keyword'] = set(nouns_list_c)
df = df[df['media'] != '코리아헤럴드'] # 코리아헤럴드는 영어 제목임
df = df[df['media'] != '주간경향'] # 주간경향은 같은 title이 많음
```
<br><br>
- Neo4j import

```
from neo4j import GraphDatabase

def add_article(tx, title, date, media, keyword):
tx.run("MERGE (a:Article {title: $title , date: $date, media: $media, keyword: $keyword})",
title=title, date=date, media=media, keyword=keyword)

def add_media(tx):
tx.run("MATCH (a:Article) "
"MERGE (b:Media {name:a.media}) "
"MERGE (a)<-[r:Publish]-(b)")

def add_keyword(tx):
tx.run("MATCH (a:Article) "
"UNWIND a.keyword as k "
"MERGE (b:Keyword {name:k}) "
"MERGE (a)-[r:Include]->(b)")

def clean_text_for_neo4j(row):
text = row['title_c']
text = re.sub(pattern='[^a-zA-Z0-9ㄱ-ㅣ가-힣]', repl='', string=text)
return text
df['title_c_neo4j'] = df.apply(clean_text_for_neo4j, axis=1)

greeter = GraphDatabase.driver("neo4j://localhost:7687", auth=("neo4j", "11thleader!"))

with greeter.session() as session:
for idx in range(len(df)):
session.write_transaction(add_article, title=df.iloc[idx]['title_c_neo4j'], date=df.iloc[idx]['date'],
media=df.iloc[idx]['media'], keyword=list(df.iloc[idx]['keyword']))
session.write_transaction(add_media)
session.write_transaction(add_keyword)
```
