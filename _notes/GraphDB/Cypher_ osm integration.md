---
title: Cypher_ osm integration
feed: show
date: 30-07-2024
---
Working With .osm Road Network Data

#### Posting information

- Posting Date : 30-07-2024  
- Last Edit : 30-07-2024  
- Writer : KWON Bongjae

#### Environment information

- Hardware : MacBookPro8,2(late 11) /  8 × Intel® Core™ i7-2675QM CPU @ 2.20GHz / RAM 15.5 GiB / Mesa Intel® HD Graphics 3000 <br>
- OS : Linux(openSUSE Tumbleweed 20240716) <br>
- DB : ArcadeDB, Neo4j Community 5.21.2 (using Cypher / openCypher) <br> 

#### Posting detail

- basic

```
import neo4j
import osmnx as ox

NEO4J_URI = "neo4j://localhost:"
NEO4J_USER = "neo4j"
NEO4J_PASSWORD = ""

driver = neo4j.GraphDatabase.driver(NEO4J_URI, auth=(NEO4J_USER, NEO4J_PASSWORD))
```
<br><br>
- Search OpenStreetMap and create a OSMNx graph

```
G = ox.graph_from_place("Busanjin-gu", network_type="drive")
fig, ax = ox.plot_graph(G)

gdf_nodes, gdf_relationships = ox.graph_to_gdfs(G)
gdf_nodes.reset_index(inplace=True)
gdf_relationships.reset_index(inplace=True)

gdf_nodes.plot(markersize=0.1)
gdf_nodes

gdf_relationships.plot(markersize=0.01, linewidth=0.5)
gdf_relationships
```
<br>
![](https://lh3.googleusercontent.com/pw/AP1GczPpwAnU1wzj09i2HaNkC43dQQbqWtDqAF0gPwtKA_aJ_ucyAMSOa1cGxFf0jQEoRyRJ4roj3WGPX1e7jjADC1718JUApNbVtOZWRgzvkP1E6NE4sZ3hIPRSLquD_Rd6D9bIP2_1ge_nK7AZnd8ns9FRCw=w794-h783-s-no?authuser=0)
<br>
- define Cypher queries to create constraints and indexes

```
constraint_query = "CREATE CONSTRAINT IF NOT EXISTS FOR (i:Intersection) REQUIRE i.osmid IS UNIQUE"

rel_index_query = "CREATE INDEX IF NOT EXISTS FOR ()-[r:ROAD_SEGMENT]-() ON r.osmids"

address_constraint_query = "CREATE CONSTRAINT IF NOT EXISTS FOR (a:Address) REQUIRE a.id IS UNIQUE"

point_index_query = "CREATE POINT INDEX IF NOT EXISTS FOR (i:Intersection) ON i.location"
```
<br>
<br>
- Query to import our road network nodes GeoDataFrame

```
node_query = '''
	UNWIND $rows AS row
	WITH row WHERE row.osmid IS NOT NULL
	MERGE (i:Intersection {osmid: row.osmid})
		SET i.location =
			point({latitude: row.y, longitude: row.x }),
				i.ref = row.ref,
				i.highway = row.highway,
				i.street_count = toInteger(row.street_count)
	RETURN COUNT(*) as total

'''
```
<br>
<br>
- Query to import our road network relationships GeoDataFrame

```
rels_query = '''
UNWIND $rows AS road
MATCH (u:Intersection {osmid: road.u})
MATCH (v:Intersection {osmid: road.v})
MERGE (u)-[r:ROAD_SEGMENT {osmid: road.osmid}]->(v)
SET r.oneway = road.oneway,
r.lanes = road.lanes,
r.ref = road.ref,
r.name = road.name,
r.highway = road.highway,
r.max_speed = road.maxspeed,
r.length = toFloat(road.length)
RETURN COUNT(*) AS total
'''
 
def create_constraints(tx):
results = tx.run(constraint_query)
results = tx.run(rel_index_query)
results = tx.run(address_constraint_query)
results = tx.run(point_index_query)

def insert_data(tx, query, rows, batch_size=10000):
total = 0
batch = 0

while batch * batch_size < len(rows):
results = tx.run(query, parameters = {'rows': rows[batch*batch_size:(batch+1)*batch_size].to_dict('records')}).data()

print(results)
total += results[0]['total']
batch += 1

with driver.session() as session:
session.execute_write(create_constraints)
session.execute_write(insert_data, node_query, gdf_nodes.drop(columns=['geometry'])) #FIXME: handle
```
<br>
<br>
- Run our relationships GeoDataFrame import

```
with driver.session() as session:

session.execute_write(insert_data, rels_query, gdf_relationships.drop(columns=['geometry'])) #FIXME: handle geometry
```
<br>
<br>
![](https://lh3.googleusercontent.com/pw/AP1GczMescJymPxr6WWiU020Ye6YIoXo16TNCdCqv2M8hBWPD0T4mqDGIjKWtfkqyvaT54YONbU3Bb1FK0cQe2ycid6o-eV5fT75U7VbUxNwmRkgDniId3KPnyAVeyNvEJm7qdw2OOBXHt4SJHmhZjqolhjd6A=w1440-h779-s-no?authuser=0)
