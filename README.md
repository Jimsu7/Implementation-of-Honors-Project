# Implementation-of-Honors-Project

The implementation of the disjoint path algorithm is in "Disjoint Path.txt", and the following is a copy of it. 
```
UNWIND range(1,10) as x // 10 is an example number of node parameter
Merge (n {id: x});
//connection
MATCH (n)
WITH collect(n) AS nodes
UNWIND nodes AS n1
UNWIND nodes AS n2
WITH n1, n2
WHERE n1 <> n2 AND rand() < 0.5 // 0.5 is an example of degree parameter to connect n1 to n2
MERGE (n1) -[:relate]-> (n2)
return n1,n2
```

The implementation of Hamiltonian path algorithm is in "Hamiltonian Path.txt", and the following is a copy of it. 
```
//Hamiltonian Path
MATCH P = (n)-[*]->(n2) // find all paths from n to n2
WITH Nodes(P) AS PathNodes
MATCH (n)
WITH collect(n) AS allnodes, PathNodes
WHERE ALL(x IN allnodes WHERE x IN PathNodes) AND size(allnodes) = size(PathNodes) //every node must appear in P and size should be equal
RETURN PathNodes LIMIT 1
```

The implementation of random graph generation is in "Random Graph Generation.txt", and the following is a copy of it. 
```
//Disjoint path
MATCH p1 = (n)-[r1*]->(n2)
MATCH p2 = (n)-[r2*]->(n2)
WHERE none(r IN relationships(p1) WHERE r IN relationships(p2)) AND id(r1[0]) < id(r2[0])
RETURN count(*)
```
