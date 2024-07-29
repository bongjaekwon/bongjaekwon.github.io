---
title: Cypher_ neo4j python driver
feed: show
date: 29-07-2024
---
Creat basic nodes and relationships

#### Posting information

- Posting Date : 29-07-2024  
- Last Edit : 29-07-2024  
- Writer : KWON Bongjae

#### Environment information

- Hardware : MacBookPro8,2(late 11) /  8 × Intel® Core™ i7-2675QM CPU @ 2.20GHz / RAM 15.5 GiB / Mesa Intel® HD Graphics 3000 <br>
- OS : Linux(openSUSE Tumbleweed 20240716) <br>
- DB : ArcadeDB, Neo4j Community 5.21.2 (using Cypher / openCypher) <br> 

#### Posting detail

```
from neo4j import GraphDatabase, RoutingControl

  
  

URI = "neo4j://localhost:7687"

AUTH = ("neo4j", "11thleader!")

  
  

def add_friend(driver, name, friend_name):

driver.execute_query(

"MERGE (a:Character {name: $name}) "

"MERGE (friend:Character {name: $friend_name}) "

"MERGE (a)-[:Is_friend_Of]->(friend)",

name=name, friend_name=friend_name, database_="neo4j",

)

  
  

def print_friends(driver, name):

records, _, _ = driver.execute_query(

"MATCH (a:Person)-[:Is_Friend_Of]->(friend) WHERE a.name = $name "

"RETURN friend.name ORDER BY friend.name",

name=name, database_="neo4j", routing_=RoutingControl.READ,

)

for record in records:

print(record["friend.name"])

  
  

with GraphDatabase.driver(URI, auth=AUTH) as driver:

add_friend(driver, "Pooh", "Piglet")

add_friend(driver, "Pooh", "Robin")

add_friend(driver, "Robin", "Alice")

print_friends(driver, "Robin")
```