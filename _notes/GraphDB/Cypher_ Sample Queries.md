---
title: Cypher_ Sample Queries
feed: show
date: 25-07-2024
---
Basic queries

#### Posting information

Posting Date : 25-07-2024  
Last Edit : 25-07-2024  
Writer : KWON Bongjae

#### Environment information

Hardware : MacBookPro8,2(late 11) /  8 × Intel® Core™ i7-2675QM CPU @ 2.20GHz / RAM 15.5 GiB / Mesa Intel® HD Graphics 3000 <br>
OS : Linux(openSUSE Tumbleweed 20240716) <br>
DB : ArcadeDB, Neo4j Community (using Cypher / openCypher) <br> 

#### Posting detail

- CREATE
	- CREATE ()
	- CREATE (a)
	- CREATE (a), (b)
	- CREATE (a:Animation)
	- CREATE (a:Animation {title: 'Winnie the Pooh'})
	- CREATE (a:Animation {title: 'Winnie the Pooh', company: 'The Walt Disney Company'})
	- CREATE (a:Animation {title: 'Winnie the Pooh'})<-[w:Written_by {when:26-10-20-1926}]-(p:Person {name: 'Alan Alexander Milne'})
<br> <br>
- MATCH
	- MATCH (a) RETURN a
	- MATCH (a:Animation) RETURN a
	- MATCH (a{title: 'Winnie the Pooh'})
	- MATCH (a:Animation {title: 'Winnie the Pooh')
	- MATCH (a{title:'Winnie the Pooh'})-(b) RETURN a, b
	- MATCH (a{title:'Winnie the Pooh'})->(b) RETURN a, b
	- MATCH (a{title:'Winnie the Pooh'})<-[w]-(p) RETURN a, type(w), p
<br> <br>
- SET
	- MATCH (c:Character {name: 'Pooh'})
	- SET c.color = 'yellow', c.born = 1921
	- RETURN c
	<br><br>
	- MATCH (c)
	- SET c:Character, c.name = 'pooh', c.color = 'yellow', c.born = 1921
	- RETURN c, labels(c)
	<br><br>
	- MATCH (c)
	- WHERE c.name = 'pooh'
	- SET c.color= 'green', c.born= 1997
	- RETURN c
	<br> <br>
	- MATCH(c)
	- WHERE c.name='pooh' AND c.color= 'green'
	- SET c = {name: 'christopher robin', age: 6}, c:Human
	- RETURN c