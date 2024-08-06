---
title: Cypher(3) MATCH use cases
feed: show
date: 27-07-2024
---
MATCH use cases

#### Posting information

Posting Date : 27-07-2024  
Last Edit : 27-07-2024  
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
- Matching nodes with relationship distances of 1 to 2
	- MATCH (c:Character)-[f:Is_Friend_Of*1..2]-(d)
	- WHERE d.name = 'Robin'
	- RETURN c, f, d
<br><br>
- Returns path by matching nodes with distances of 1 to 2
	- MATCH (c:Character)-[f:Is_Friend_Of*1..2]-(d)
	- WHERE d.name = 'Robin'
	- RETURN path
<br><br>
- shortestPath()
	- MATCH path = shortestPath((c:Character)-[*]->(d))
	- WHERE c.name = 'Pooh' AND d.name = 'Robin'
	- RETURN path
<br><br>
- Return relationship & node types by matching nodes with distances of 1 to 2
	- MATCH path = (c:Character)-[f:Is_Friend_Of*1..2]-(d)
	- WHERE c.name = 'Pooh'
	- RETURN c, [rel in relationships(path)] | type(rel)], d
<br><br>
- OPTIONAL MATCH
	- MATCH path = (c:Character)-[f:Is_Friend_Of*1..2]-(d)
	- WHERE c.name = 'Pooh'
	- OPTIONAL MATCH (d)-[:Is_Family_Of]-(e)
	- RETURN c, f, d, e
<br><br>
- ORDER BY
	- MATCH path = (c:Character)-[f:Is_Friend_Of*1..2]-(d)
	- WHERE c.name = 'Pooh'
	- RETURN DISTINCT d.name, c.age
	- ORDER BY d.age
<br><br>
- ORDER BY - DESC
	- MATCH path = (c:Character)-[f:Is_Friend_Of*1..2]-(d)
	- WHERE c.name = 'Pooh'
	- RETURN DISTINCT d.name, c.age
	- ORDER BY d.age DESC
<br><br>
- SKIP
	- MATCH path = (c:Character)-[f:Is_Friend_Of*1..2]-(d)
	- WHERE c.name = 'Pooh'
	- RETURN DISTINCT d.name, c.age
	- ORDER BY d.age DESC
	- SKIP 2
<br><br>
- LIMIT
	- MATCH path = (c:Character)-[f:Is_Friend_Of*1..2]-(d)
	- WHERE c.name = 'Pooh'
	- RETURN DISTINCT d.name, c.age
	- ORDER BY d.age DESC
	- SKIP 2
	- LIMIT 3
<br><br>
- ALL()
	- MATCH path = (c:Character)-[f:Is_Friend_Of*1..2]-(d)
	- WHERE c.name = 'Pooh' AND ALL (x IN nodes(path) WHERE x.age > 5)
	- RETURN DISTINCT c.name, d.name, d.age
<br><br>
- length()
	- MATCH path = (c:Character)-[f:Is_Friend_Of*1..2]-(d)
	- WHERE c.name = 'Pooh'
	- RETURN length(path)
<br><br>
- nodes(), relationships() - Extracting nodes or relationships that exist in path
	- MATCH path = (c:Character)-[f:Is_Friend_Of*1..2]-(d)
	- WHERE EXISTS(c.name)
	- RETURN nodes(path), relationships(path)
<br><br>
- head(), last()
	- MATCH path = (c:Character)-[f:Is_Friend_Of*1..2]-(d)
	- WHERE c.name = 'Pooh'
	- WITH nodes(path) as chracter_list
	- RETURN character_list, head(chracter_list).name, last(chracter_list).name
<br><br>
- head(), last() 2
	- MATCH path = (c:Character)-[f:Is_Friend_Of*1..2]-(d)
	- WHERE c.name = 'Pooh'
	- WITH [l in nodes(path) '|' l.name] as Character_list
	- RETURN character_list, head(chracter_list).name, last(chracter_list).name
<br><br>