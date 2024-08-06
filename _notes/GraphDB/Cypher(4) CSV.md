---
title: Cypher(4) CSV
feed: hide
date: 28-07-2024
---
CSV use

#### Posting information

Posting Date : 28-07-2024  
Last Edit : 28-07-2024  
Writer : KWON Bongjae

#### Environment information

Hardware : MacBookPro8,2(late 11) /  8 × Intel® Core™ i7-2675QM CPU @ 2.20GHz / RAM 15.5 GiB / Mesa Intel® HD Graphics 3000 <br>
OS : Linux(openSUSE Tumbleweed 20240716) <br>
DB : ArcadeDB, Neo4j Community 5.21.2 (using Cypher / openCypher) <br> 

#### Posting detail

'file://Pooh_character.csv' (UTF-8)

| no  | name   | animal   | actor |
| --- | ------ | -------- | ----- |
| 1   | Pooh   | bear     | 송도영   |
| 2   | Tigger | tiger    | 설영범   |
| 3   | Piglet | pig      | 이진화   |
| 4   | Eeyore | donkey   | 김정호   |
| 5   | Rabbit | rabbit   | 장광    |
| 6   | Robin  | human    | 이대원   |
| 7   | Kanga  | kangaroo | 임은정   |
| 8   | Roo    | kangaroo | 최덕희   |
| 9   | Owl    | owl      | 이재명   |
| 10  | Gopher | gopher   | 박지훈   |

<br><br>
- Read as line - the result is in lists
	- LOAD CSV FROM 'file:///Pooh_character.csv' AS line
	- RETURN line
<br><br>
- linenumber()
	- LOAD CSV FROM 'file:///Pooh_character.csv' AS line
	- RETURN linenumber() AS number, line
<br><br>
- HEADER
	- LOAD CSV WITH HEADERS FROM 'file:///Pooh_character.csv' AS line
	- RETURN linenumber() AS number, line
<br><br>
- RETURN VALUE
	- LOAD CSV WITH HEADERS FROM 'file:///Pooh_character.csv' AS line
	- RETURN line.name
<br><br>
- nodes & relationships creation
	- LOAD CSV WITH HEADERS FROM 'file:///Pooh_character.csv' AS line
	- CREATE (:Character {name:line.name})-[:Is_Acted_By]->(:Actor{name:line.actor})
<br><br>![Screenshot](https://lh3.googleusercontent.com/pw/AP1GczOZAqQ9836BvkLxjC2zdggIAtp8ysfjpIe73KfxIOzfx9KkXnC0Zz_U149rf8ye1V0sX-wxb2aEttRp2b-sT6RgCHnJJ8SDeNExiu40pVzK5h9X1sllU88cVnUvYriNx46AV5awJomJNPCsJfkc5wdyGQ=w1253-h783-s-no?authuser=0)