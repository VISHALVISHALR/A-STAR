<h1>ExpNo 4 : Implement A* search algorithm for a Graph</h1> 
<h3>Name:   R.VISHAL    </h3>
<h3>Register Number:  212224040363         </h3>
<H3>Aim:</H3>
<p>To ImplementA * Search algorithm for a Graph using Python 3.</p>
<H3>Algorithm:</H3>

``````
// A* Search Algorithm
1.  Initialize the open list
2.  Initialize the closed list
    put the starting node on the open 
    list (you can leave its f at zero)

3.  while the open list is not empty
    a) find the node with the least f on 
       the open list, call it "q"

    b) pop q off the open list
  
    c) generate q's 8 successors and set their 
       parents to q
   
    d) for each successor
        i) if successor is the goal, stop search
        
        ii) else, compute both g and h for successor
          successor.g = q.g + distance between 
                              successor and q
          successor.h = distance from goal to 
          successor (This can be done using many 
          ways, we will discuss three heuristics- 
          Manhattan, Diagonal and Euclidean 
          Heuristics)
          
          successor.f = successor.g + successor.h

        iii) if a node with the same position as 
            successor is in the OPEN list which has a 
           lower f than successor, skip this successor

        iV) if a node with the same position as 
            successor  is in the CLOSED list which has
            a lower f than successor, skip this successor
            otherwise, add  the node to the open list
     end (for loop)
  
    e) push q on the closed list
    end (while loop)

``````

<hr>
<h2>Sample Graph I</h2>
<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/b1377c3f-011a-4c0f-a843-516842ae056a)

PROGRAM :
```
from collections import defaultdict

#Constructing a weighted graph
def astar(start,goal):
    #pass
    #having 2 queues - open and closed
    openset=set(start)
    closed=set()
    g = {}
    parents = {}
    g[start] = 0
    parents[start] = start
    while (len(openset)>0):
        n = None
        for v in openset:
            if n==None or g[v]+heuristic(v)<g[n]+heuristic(n):
                n=v
        if (n==goal or graph_nodes[n]==None): #if we reach goal node or all nodes are traversed
            pass
        else:
            for (m,weight) in getneighbours(n):
                if m not in openset and m not in closed:
                    openset.add(m)
                    parents[m] = n
                    g[m] = g[n] + weight
                else:
                    if (g[m]>g[n]+weight):
                        g[m]=g[n]+weight
                        parents[m]=n
                        if m in closed:
                            closed.remove(m)
                            openset.add(m)
        if(n==None):
            return None
        #if goal is reached move from goal node to start node--->path
        if (n==goal):
            path=[]
            while parents[n]!=n:
                path.append(n)
                n=parents[n]
            path.append(start)
            path.reverse()
            print(path)
            return path
        closed.add(n)
        openset.remove(n)
    return None
            
def getneighbours(n):
    if(n in graph_nodes):
        return graph_nodes[n]
    else:
        return None
def heuristic(n):
    return H_dist[n]
graph = defaultdict(list)
H_dist = {}
nodes,edges = map(int,input().split())
for i in range(edges):
    u,v,cost = map(str,input().split())
    t = (u,float(cost))
    graph[v].append(t)
    t1 = (v,float(cost))
    graph[u].append(t1)
print(graph)
graph_nodes=graph
for i in range(nodes):
    node,h = map(str,input().split())
    H_dist[node] = float(h)
print(H_dist)
start = input()
goal = input()
print(getneighbours(start))
print(heuristic(start))
print(heuristic(goal))
astar(start,goal)
```

<hr>
<h2>Sample Input</h2>
<hr>
10 14 <br>
A B 6 <br>
A F 3 <br>
B D 2 <br>
B C 3 <br>
C D 1 <br>
C E 5 <br>
D E 8 <br>
E I 5 <br>
E J 5 <br>
F G 1 <br>
G I 3 <br>
I J 3 <br>
F H 7 <br>
I H 2 <br>
A 10 <br>
B 8 <br>
C 5 <br>
D 7 <br>
E 3 <br>
F 6 <br>
G 5 <br>
H 3 <br>
I 1 <br>
J 0 <br>
<hr>
<h2>Sample Output</h2>
<img width="418" height="746" alt="image" src="https://github.com/user-attachments/assets/8a35de2c-eb66-4e78-ba97-e1cd1fca178e" />
<img width="698" height="184" alt="image" src="https://github.com/user-attachments/assets/ad6ae288-c9ec-45b0-a41a-7b76d6fbed64" />

<hr>
Path found: ['A', 'F', 'G', 'I', 'J']


<hr>
<h2>Sample Graph II</h2>
<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/acbb09cb-ed39-48e5-a59b-2f8d61b978a3)


<hr>
<h2>Sample Input</h2>
<hr>
6 6 <br>
A B 2 <br>
B C 1 <br>
A E 3 <br>
B G 9 <br>
E D 6 <br>
D G 1 <br>
A 11 <br>
B 6 <br>
C 99 <br>
E 7 <br>
D 1 <br>
G 0 <br>
<hr>
<h2>Sample Output</h2>
<img width="695" height="322" alt="image" src="https://github.com/user-attachments/assets/d5013135-c668-4799-ab65-9b82930ec2c0" />

<hr>
Path found: ['A', 'E', 'D', 'G']
