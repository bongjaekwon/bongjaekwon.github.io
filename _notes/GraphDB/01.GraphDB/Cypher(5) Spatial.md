---
title: Cypher(5) Spatial
feed: hide
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

- CREATE
	- CREATE (y:University {longitude: 126.93691, latitude: 37.56025, name: 'Yonsei university'}), (s:University {longitude: 126.95195, latitude: 37.45263, name: 'Seoul national university'}), (y)-[:From_to]->(s)
<br><br>
- point.distance()
	- point.distance(point1, point2) 
	- return type is FLOAT** <br><br>
	- WITH point({x: 2.3, y: 4.5, crs: 'cartesian'}) AS p1, point({x: 1.1, y: 5.4, crs: 'cartesian'}) AS p2
	- RETURN point.distance(p1,p2) AS distance 
	- distance between 2d points**<br><br> 
	- WITH point({longitude: 12.78, latitude: 56.7, height: 100}) AS p1, point({latitude: 56.71, longitude: 12.79, height: 100}) AS p2
	- RETURN point.distance(p1,p2) AS distance
	- distance between 3d points**<br><br>
	- MATCH (y:University{name:'Yonsei university'})-[:From_to]->(s:University{name:'Seoul national university'})
	- WITH point({longitude: y.longitude, latitude: y.latitude}) AS PointYonsei, point({longitude: s.longitude, latitude: s.latitude}) AS PointSNU
	- RETURN round(point.distance(PointYonsei, PointSNU)) AS GraduateDistance
<br><br> 
- point.withinBBox()
	- point.withinBBox(point, lowerLeft, upperRight)
	- return type is BOOLEAN** <br><br>
	- WITH point({x: 0, y: 0, crs: 'cartesian'}) AS lowerLeft, point({x: 10, y: 10, crs: 'cartesian'}) AS upperRight
	- RETURN point.withinBBox(point({x: 5, y: 5, crs: 'cartesian'}), lowerLeft, upperRight) AS result
	- return value is TRUE**<br><br> 
	- WITH point({longitude: 124, latitude: 33}) AS lowerLeft, point({longitude: 132, latitude: 43}) AS upperRight
	- MATCH (u:University)
	- WHERE point.withinBBox(point({longitude: u.longitude, latitude: u.latitude}), lowerLeft, upperRight) 
	- RETURN count()
	- finds all universities in  a bounding box around Korea** 
<br> <br>
- point()
	- RETURN point({longitude: 127, latitude: 34}) AS point
	- RETURN point({longitude: 127, latitude: 34, crs: 'WGS-84'}) AS point <br><br>
	- MATCH (u:University) 
	- RETURN point({longitude: u.longitude, latitude: u.latitude, crs: 'WGS-84'}) AS universityPoint 
	- point({srid:4326, x:126.93691, y:37.56025})**
	- point({srid:4326, x:126.95195, y:37.45263})**