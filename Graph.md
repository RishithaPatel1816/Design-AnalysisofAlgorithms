# GRAPHS
## Representing Graphs
- We can represent graphs in multiple ways.
- We will be following adjancency list.This is vector of vector all the vertices in graph with their adjacent vertices.
![image](https://github.com/user-attachments/assets/b98106c2-9423-49f2-805c-06b175863b0d)
- We will first learn two basic algorithms of Graphs.They are **BFS & DFS**.
##  Breadth-first Search
- Let G=(V,E) be a graph with set of vertices V and edge set E.We want to discover all the verticies that are reachable from node s.
- Once the BFS is performed, for every vertex v in the graph G, path from s to v will be the shortest path(least number of edges required to traverse from s to u.
- We discover the nodes breadth wise.It is like starting from s we discover vertices that are at distance 1 then at distance 2 and so on.If at all a vertex is not reachable from s then it can't be visoted through BFS.
- We will use a queue to implement this which uses a first in first out principle.
- We will have colors for u vertices initialized to white then turn them to grey when they are in queue and turn them to black when it is completely covered.
- Breadth first search gives u a breadth first tree with root as s.When we discover v through edge (u,v) we say that u is parent/predecessor of v.
- If we have a path from u to v in the tree then we say u is ancestor of v and v is ancestor of u.
- so we define
    - v.color : color of vertex can be white grey or black
    - v.d     : distance from source vertex s
    - v.p     : is the parent of v is the dfs tree.
- Intially all vertices vbelpngs to V, v.color = white, v.d = Infinity, v.p = NIL.
```Pseudo Code
BFS(G,s)
  for each vertex u in G.V - {s}
    u.color = White
    u.d = Infinity
    u.p = NIL
  s.color=gray
  s.d=0
  Q.push(s)
  while q is not empty
    u=deque(Q)
    for all vertices v that are adjacent to u
      if v.color=white
        v.d=u.d+1
        v.color=grey
        Q.push(v)
    u.color = black
```
- The resultant BFS tree depends in which oreder we the neighbours of given vertex are visited but d remains same.
### Running Time
- Each vertex is enqueued atmost once and and after initialization BFS never whitens a vertex so we dequeu it once so O(V+E) is the runnint time of the algorithm.
### Shortest paths through BFS
- **Shortest Path** : The minimum number of edges required from agiven vertex s to reach the vertex v.
- Our claim is that BFS gives shortest path for all the vertices.We need to prove it now.
- Let's see the following lemmas that will be useful in proofs
#### Lemmma 1
- For a graph G = (V,E) is an undirected/directed graph and let s belong to v and for any arbitary edge (u,v) in E  is δ(s,v)<=δ(s,u)+1
###### Proof:
- Let's take two cases
    - Case 1: u is visited through u. Then δ(s,v)=δ(s,u)+1 so the equation holds true.
    - Case 2: u is not visited through u, then v must be visited before discovering u , so δ(s,v)<=δ(s,u) hence proved.
#### Lemmma 2
- For a graph G = (V,E) is an undirected/directed graph and let BFS is run from vertex s in V. Then for each vertec v in V, the value v.d computed by BFS satisfies v.d>δ(s,v) at all the times including termination.
###### Proof:
- We will use induction on number of enqueue operations
- Base case : enqueuing s-> s.d=0 and rem dist is infinity so condition holds true here.
- Induction : let v be a vertex found when search from u, u.d>=δ(s,u) and v.d=infinity >= δ(s,v_ for all v in V-{s}
- v.d = u.d + 1 >= δ(s,u) + 1 > δ(s,v)
- Hence proved
#### Lemmma 3
- During the execution of BFS on graph G = (V,E), the queue has vertices (v1,v2,...,vr) where v1 is the head and vr is the tail.Then vr.d<=v1.d+1 and vi.d<=vi+1.d for i= 1 to r-1













