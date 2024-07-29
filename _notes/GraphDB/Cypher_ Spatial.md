---
title: Cypher_ Spatial
feed: show
date: 29-07-2024
---
Handling spatial values & functions

#### Posting information

- Posting Date : 29-07-2024  
- Last Edit : 29-07-2024  
- Writer : KWON Bongjae

#### Environment information

- Hardware : MacBookPro8,2(late 11) /  8 × Intel® Core™ i7-2675QM CPU @ 2.20GHz / RAM 15.5 GiB / Mesa Intel® HD Graphics 3000 <br>
- OS : Linux(openSUSE Tumbleweed 20240716) <br>
- DB : ArcadeDB, Neo4j Community 5.21.2 (using Cypher / openCypher) <br> 

#### Posting detail
<br>
- CREATE
	- CREATE (y:University {longitude: 126.93691, latitude: 37.56025, name: 'Yonsei university'}), (s:University {longitude: 126.95195, latitude: 37.45263, name: 'Seoul national university'}), (y)-[:From_to]->(s)
<br><br>
- point.distance()
	- 