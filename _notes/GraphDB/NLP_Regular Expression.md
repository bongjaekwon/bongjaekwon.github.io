---
title: NLP_Regular Expression
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

```