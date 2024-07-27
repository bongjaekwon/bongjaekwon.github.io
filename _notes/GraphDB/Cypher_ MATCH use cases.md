---
title: Cypher_ MATCH use cases
feed: show
date: 27-07-2024
---
MATCH use cases

#### Posting information

Posting Date : 25-07-2024  
Last Edit : 25-07-2024  
Writer : KWON Bongjae

#### Environment information

Hardware : MacBookPro8,2(late 11) /  8 × Intel® Core™ i7-2675QM CPU @ 2.20GHz / RAM 15.5 GiB / Mesa Intel® HD Graphics 3000 <br>
OS : Linux(openSUSE Tumbleweed 20240716) <br>
DB : ArcadeDB, Neo4j Community 5.21.2 (using Cypher / openCypher) <br> 

#### Posting detail

- Matching with multiple properties
	- MATCH (c:Character{age:6, name:'Robin'})
	- RETURN c.name
<br><br>
- Properties value comparison
	- MATCH (c:Chracter)
	- WHERE c.age >5
	- RETURN c.name, c.age
<br><br>
- AND / OR
	- AND**
	- MATCH (c:Character)-[:Is_Friend_Of]->(d:Character)
	- WHERE c.age=1 AND c.color="yellow"
	- RETURN c.name, c.age
	- OR**	
	- MATCH (c:Character)-[:Is_Friend_Of]->(d:Character)
	- WHERE c.age=1 OR c.age=5
	- RETURN c.name, c.age
<br><br>
- IS NULL / IS NOT NULL
	- MATCH (c:Character)
	- WHERE c.age IS NOT NULL
	- RETURN c
<br><br>
- EXISTS / NOT EXISTS
	- MATCH (c:Character)
	- WHERE EXISTS ( (c)-[:Is_Friend_Of]-> () )
	- RETURN c
<br><br>
- COUNT
	- MATCH (c:Character)-[:Is_Friend_Of]->(d:Character)
	- WHERE d.name = 'Robin'
	- RETURN count(c)
<br><br>
- STARTS WITH
	- MATCH (c:Character)
	- WHERE c.name STARTS WITH 'R'
	- RETURN c
<br><br>
- IN []
	- MATCH (c:Character)
	- WHERE c.age IN [1, 2, 3, 4, 5]
	- RETURN c, c.age as age
<br><br>
- COLLECT() --> return in list form
	- MATCH (c:Character)
	- RETURN COLLECT(c.name)
<br><br>
- Matching by the distance between nodes
	- MATCH (c:Character)-[f:Is_Friend_Of*1]-(d)
	- WHERE d.name = 'Robin'
	- RETURN c, d
<br><br>