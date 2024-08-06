---
title: Cypher(1) Basic
feed: show
date: 24-07-2024
---
The concept of Cypher

#### Posting information

Posting Date : 24-07-2024  
Last Edit : 24-07-2024  
Writer : KWON Bongjae

#### Environment information

Hardware : MacBookPro8,2(late 11) /  8 × Intel® Core™ i7-2675QM CPU @ 2.20GHz / RAM 15.5 GiB / Mesa Intel® HD Graphics 3000 <br>
OS : Linux(openSUSE Tumbleweed 20240716) <br>
DB : ArcadeDB, Neo4j Community (using Cypher / openCypher) <br> 

#### Posting detail

This posting is about introducing Cypher and a NoSQL-based database that uses Cypher. Cypher is basically a 'declarative' 'graph' query language. Based on the Property Graph model, standard graph elements of nodes and edge-relationship- are the main concepts, and they have labels and properties. Properties consist of string keys and some value key-value bindings in the cypher data type. 

The basic structure of this query languae is summarized as follows.

> [!NOTE] Nodes () (variable) (:label) (variable :label1 : label2) ...
> - id
> - label
> - properties map

> [!NOTE] Relationships (n1)-[variable name: type name {attribute key 1:"attribute value", attribute key 2:"attribute value"}]->(n2)
> - id
> - type
> - properties map
> - node id
>

> [!NOTE] Path
> - Nodes - Relationships sequence

> [!NOTE] ---Clauses
> - MATCH
> - OPTIONAL MATCH
> - RETURN
> - WHERE
> - WITH
> - CREATE
> - SET
> - MERGE
> - UNWIND
> - ORDER BY
> - SKIP 
> - LIMIT
> - DELETE
> - REMOVE
> - UNION
> - USE
> - LOAD CSV
> - FOREACH
> - CALL {} (subquery)
> - CALL procedure




Cypher
```
MERGE (c:Chracter {name: 'Pooh'})-[:Is_character_of]->(a:animation {name: 'Winnie the Pooh'})

RETURN c, a
```



ArcadeDB
![ArcadeDB](https://lh3.googleusercontent.com/pw/AP1GczPyXBpF5fe_UV-JXVy3E0fPGDF33eIJW7s3W97UolZuaDoE0c6nUA-J8JBoznH1xERGRRfdHMRIIF_G9k6S4Rzi3yTuMETs4iABnyZ6iDJGX2b3gELqNl24672u7uy2X8HHKI-JJ9C698wRGK0k9fhfIg=w1253-h783-s-no?authuser=0)


Neo4j
![ArcadeDB](https://lh3.googleusercontent.com/pw/AP1GczNJ8Cy2AbuLQ9imaFWRgg4wArJ9-D8yIn6nf5JA_LjduYKx6mzXKXMEJS-tvFg96qVxnGgfwXZglJI1fYKK7SmU5MaPFlXMRXWfi83HA37oaw8J3T_a42kihePM2ZEpmiAC0trh5wCrvg7J5LG2CFtXOQ=w1253-h783-s-no?authuser=0)
