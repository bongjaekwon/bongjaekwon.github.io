---
title: Cypher_ osm to neo4j
feed: show
date: 29-07-2024
---
Create basic nodes and relationships

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

  
  

URI = "neo4j://localhost:   "

AUTH = ("   ", "   ")

  
  

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
<br>
<br>
```
import logging

  

from neo4j import GraphDatabase, RoutingControl

from neo4j.exceptions import DriverError, Neo4jError

  
  

class App:

  

def __init__(self, uri, user, password, database=None):

self.driver = GraphDatabase.driver(uri, auth=(user, password))

self.database = database

  

def close(self):

self.driver.close()

  

def create_friendship(self, chracter_1, charcter_2):

with self.driver.session() as session:

result = self._create_and_return_friendship(

chracter_1, charcter_2

)

print("Created friendship between: "

f"{result['p1']}, {result['p2']}")

  

def _create_and_return_friendship(self, character_1, character_2):

  

query = (

"CREATE (c1:Character { name: $character_1 }) "

"CREATE (c2:Chracter { name: $character_2 }) "

"CREATE (c1)-[:KNOWS]->(c2) "

"RETURN c1.name, c2.name"

)

try:

record = self.driver.execute_query(

query, character_1=character_1, character_2=character_2,

database_=self.database,

result_transformer_=lambda r: r.single(strict=True)

)

return {"p1": record["c1.name"], "p2": record["c2.name"]}

except (DriverError, Neo4jError) as exception:

logging.error("%s raised an error: \n%s", query, exception)

raise

  

def find_character(self, character_name):

names = self._find_and_return_person(character_name)

for name in names:

print(f"Found character: {name}")

  

def _find_and_return_person(self, character_name):

query = (

"MATCH (p:Person) "

"WHERE p.name = $character_name "

"RETURN p.name AS name"

)

names = self.driver.execute_query(

query, character_name=character_name,

database_=self.database, routing_=RoutingControl.READ,

result_transformer_=lambda r: r.value("name")

)

return names

  

if __name__ == "__main__":

scheme = "neo4j"

host_name = "localhost"

port = 7687

uri = f"{scheme}://{host_name}:{port}"

user = "neo4j"

password = "   "

database = "   "

app = App(uri, user, password, database)

try:

app.create_friendship("Pooh", "Robin")

app.find_character("Pooh")

finally:

app.close()
```