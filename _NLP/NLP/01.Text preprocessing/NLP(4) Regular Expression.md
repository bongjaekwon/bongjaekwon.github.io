---
title: NLP(4) Regular Expression
feed: show
date: 03-08-2024
---
#### Posting information

- Posting Date : 03-08-2024  
- Last Edit : 03-08-2024  
- Writer : KWON Bongjae

#### Posting detail

```
#01_04 : Regular Expression

  

import re

  

#1) .

  

r = re.compile("p..h")

r.search("pooh") #<re.Match object; span=(0, 4), match='pooh'>

r.search("oooo") # nothing printed

  

#2) ?

  

r=re.compile("poo?h")

r.search("pooh") #<re.Match object; span=(0, 4), match='pooh'>

r.search("poh") #<re.Match object; span=(0, 3), match='poh'>

r.search("pooh") # nothing printed

  

#3) *

  

r=re.compile("poo*h")

r.search("poh") #<re.Match object; span=(0, 2), match='ph'>

r.search("pooh") #<re.Match object; span=(0, 4), match='pooh'>

r.search("poooh") #<re.Match object; span=(0, 5), match='poooh'>

  

#4) +

  

r=re.compile("poo+h")

r.search("poh") #nothing returned

r.search("pooh") #<re.Match object; span=(0, 4), match='pooh'>

r.search("poooh") #<re.Match object; span=(0, 5), match='poooh'>

  

#5) ^

  

r=re.compile("^p")

r.search("owl") #nothing returned

r.search("robin") #nothing returned

r.search("piglet") #<re.Match object; span=(0, 1), match='p'>

r.search("pooh") #<re.Match object; span=(0, 1), match='p'>

  

#6) {number}

  

r=re.compile("po{2}h")

r.search("poh") #nothing returned

r.search("pooh") #<re.Match object; span=(0, 4), match='pooh'>

r.search("poooh") #nothing returned

  

#7) {number1, number2}

  

r=re.compile("po{2,3}h")

r.search("poh") #nothing returned

r.search("pooh") #<re.Match object; span=(0, 4), match='pooh'>

r.search("poooh") #<re.Match object; span=(0, 5), match='poooh'>

  

#8) {number,}

  

r=re.compile("po{2,}h")

r.search("poh") #nothing returned

r.search("pooh") #<re.Match object; span=(0, 4), match='pooh'>

r.search("pooooooooooooooooh") #<re.Match object; span=(0, 18), match='pooooooooooooooooh'>

  

#9) []

  

r=re.compile("[p]")

r.search("ropin") #<re.Match object; span=(2, 3), match='p'>

r.search("robin") #nothing returned

r.search("pooh") #<re.Match object; span=(0, 1), match='p'>

r.search("booh") #nothing returned

  

r=re.compile("[a-c]")

r.search("robin") #<re.Match object; span=(2, 3), match='b'>

r.search("pooh") #nothing returned

r.search("piglet") #nothing returned

r.search("kangga") #<re.Match object; span=(1, 2), match='a'>

  

#10) [^character]

  

r=re.compile("[^abc]")

r.search("aamilne") #<re.Match object; span=(2, 3), match='m'>

r.search("aapilne") #<re.Match object; span=(2, 3), match='p'>

  
  

#function

  

#1) re.match(), re.search()

  

r=re.compile("pooh")

r.match("poohandpiglet") #<re.Match object; span=(0, 4), match='pooh'>

r.match("pigletandpooh") #nothing returned

  

r.search("poohandpiglet") #<re.Match object; span=(0, 4), match='pooh'>

r.search("pigletandpooh") #<re.Match object; span=(9, 13), match='pooh'>

  

#2) re.split()

  

#split by empty space

character = "pooh piglet owl kangga gopher robin"

re.split(" ", character) #['pooh', 'piglet', 'owl', 'kangga', 'gopher', 'robin']

  

#split by \n

character = """pooh

piglet

owl

kangga

gopher

robin"""

#['pooh', 'piglet', 'owl', 'kangga', 'gopher', 'robin']

  

character = "pooh+piglet+owl+kangga+gopher+robin"

re.split("\+", character)

#['pooh', 'piglet', 'owl', 'kangga', 'gopher', 'robin']

  

#3) re.findall()

  

character = """ name : pooh

born : 1997 - 11 - 10

age : 28

sex : male"""

  

re.findall("\d+", character)

#['1997', '11', '10', '28']

  
  

#4) re.sub()

story = """If you happen to have read another book about Christopher Robin, you may

remember that he once had a swan (or the swan had Christopher Robin, I

don't know which) and that he used to call this swan Pooh. That was a

long time ago, and when we said good-bye, we took the name with us, as

we didn't think the swan would want it any more. Well, when Edward Bear

said that he would like an exciting name all to himself, Christopher

Robin said at once, without stopping to think, that he was

Winnie-the-Pooh. And he was. So, as I have explained the Pooh part, I

will now explain the rest of it."""

  

preprocessed_story = re.sub('[^a-zA-Z]', ' ', story)

print(preprocessed_story)

#If you happen to have read another book about Christopher Robin you may remember that he once had a swan or the swan had Christopher Robin I don t know which and that he used to call this swan Pooh That was a long time ago and when we said good bye we took the name with us as we didn t think the swan would want it any more Well when Edward Bear said that he would like an exciting name all to himself Christopher Robin said at once without stopping to think that he was Winnie the Pooh And he was So as I have explained the Pooh part I will now explain the rest of it

  
  

#regular expression example

character = """001 pooh bear YELLOW

002 piglet pig PINK

003 tigger tiger RED"""

  

result1 = re.split('\s+', character)

print(result1) #['001', 'pooh', 'bear', 'YELLOW', '002', 'piglet', 'pig', 'PINK', '003', 'tigger', 'tiger', 'RED']

  

result2 = re.findall('\d+', character)

print(result2) #['001', '002', '003']

  

result3 = re.findall('[A-Z]', character)

print(result3) #['Y', 'E', 'L', 'L', 'O', 'W', 'P', 'I', 'N', 'K', 'R', 'E', 'D']

  

result4 = re.findall('[A-Z]{3,}', character)

print(result4) #['YELLOW', 'PINK', 'RED']

  
  

#tokenization with regular expression

from nltk.tokenize import RegexpTokenizer

  

story = """If you happen to have read another book about Christopher Robin, you may

remember that he once had a swan (or the swan had Christopher Robin, I

don't know which) and that he used to call this swan Pooh. That was a

long time ago, and when we said good-bye, we took the name with us, as

we didn't think the swan would want it any more. Well, when Edward Bear

said that he would like an exciting name all to himself, Christopher

Robin said at once, without stopping to think, that he was

Winnie-the-Pooh. And he was. So, as I have explained the Pooh part, I

will now explain the rest of it."""

  

tokenizer1 = RegexpTokenizer("[\w]+")

print(tokenizer1.tokenize(story))

#['If', 'you', 'happen', 'to', 'have', 'read', 'another', 'book', 'about', 'Christopher', 'Robin', 'you', 'may', 'remember', 'that', 'he', 'once', 'had', 'a', 'swan', 'or', 'the', 'swan', 'had', 'Christopher', 'Robin', 'I', 'don', 't', 'know', 'which', 'and', 'that', 'he', 'used', 'to', 'call', 'this', 'swan', 'Pooh', 'That', 'was', 'a', 'long', 'time', 'ago', 'and', 'when', 'we', 'said', 'good', 'bye', 'we', 'took', 'the', 'name', 'with', 'us', 'as', 'we', 'didn', 't', 'think', 'the', 'swan', 'would', 'want', 'it', 'any', 'more', 'Well', 'when', 'Edward', 'Bear', 'said', 'that', 'he', 'would', 'like', 'an', 'exciting', 'name', 'all', 'to', 'himself', 'Christopher', 'Robin', 'said', 'at', 'once', 'without', 'stopping', 'to', 'think', 'that', 'he', 'was', 'Winnie', 'the', 'Pooh', 'And', 'he', 'was', 'So', 'as', 'I', 'have', 'explained', 'the', 'Pooh', 'part', 'I', 'will', 'now', 'explain', 'the', 'rest', 'of', 'it']

  

tokenizer2 = RegexpTokenizer("\s+", gaps=True)

tokenizer3 = RegexpTokenizer("\s+", gaps=False)

print(tokenizer2.tokenize(story))

#['If', 'you', 'happen', 'to', 'have', 'read', 'another', 'book', 'about', 'Christopher', 'Robin,', 'you', 'may', 'remember', 'that', 'he', 'once', 'had', 'a', 'swan', '(or', 'the', 'swan', 'had', 'Christopher', 'Robin,', 'I', "don't", 'know', 'which)', 'and', 'that', 'he', 'used', 'to', 'call', 'this', 'swan', 'Pooh.', 'That', 'was', 'a', 'long', 'time', 'ago,', 'and', 'when', 'we', 'said', 'good-bye,', 'we', 'took', 'the', 'name', 'with', 'us,', 'as', 'we', "didn't", 'think', 'the', 'swan', 'would', 'want', 'it', 'any', 'more.', 'Well,', 'when', 'Edward', 'Bear', 'said', 'that', 'he', 'would', 'like', 'an', 'exciting', 'name', 'all', 'to', 'himself,', 'Christopher', 'Robin', 'said', 'at', 'once,', 'without', 'stopping', 'to', 'think,', 'that', 'he', 'was', 'Winnie-the-Pooh.', 'And', 'he', 'was.', 'So,', 'as', 'I', 'have', 'explained', 'the', 'Pooh', 'part,', 'I', 'will', 'now', 'explain', 'the', 'rest', 'of', 'it.']

print(tokenizer3.tokenize(story))

#[' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', '\n', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', '\n', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', '\n', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', '\n', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', '\n', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', '\n', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', '\n', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', '\n', ' ', ' ', ' ', ' ', ' ', ' ']
```