
# EX 5E Minimum Spanning Tree -Boruvka's Algorithm
## DATE: 16-11-2025
## AIM:
To write a Java program to for given constraints.
Boruvka's Algorithm - Minimum Spanning Tree

Find the MST using Boruvka's Algorithm for a weighted undirected graph.
<img width="292" height="235" alt="image" src="https://github.com/user-attachments/assets/06246b27-37a9-40a8-bd7a-37a1d5187cd1" />

## Algorithm
1. Initialize each vertex as its own disjoint set using a parent array.  
2. Repeatedly find the cheapest outgoing edge for every component.  
3. For each component, add its cheapest edge to the MST if it connects two different components.  
4. Union the components connected by the chosen edges and update the MST weight.  
5. Repeat until only one component remains or no more edges can be added.

#### Developed By: Mohamed Hameem Sajith J
#### Register Number: 212223240090

## Program:
```java
import java.util.*;

public class BoruvkaMST {
    static int[] parent;

    static int find(int i) {
        if (parent[i] != i)
            parent[i] = find(parent[i]);
        return parent[i];
    }

    static void union(int x, int y) {
        parent[find(x)] = find(y);
    }

    
    static int boruvkaMST(int V, List<Edge> edges) {
        //Type your code here
        parent=new int[V];
        for(int i=0;i<V;i++)parent[i]=i;
        
        int numv=V;
        int mw=0;
        
        while(numv>1){
            Edge[] cheapest=new Edge[V];
            
            for(Edge e:edges){
                int set1=find(e.src);
                int set2=find(e.dest);
                
                if(set1==set2)continue;
                
                if(cheapest[set1]==null || e.weight<cheapest[set1].weight){
                    cheapest[set1]=e;
                }
                if(cheapest[set2]==null || e.weight<cheapest[set2].weight){
                    cheapest[set2]=e;
                }
            }
            
            boolean added=false;
            
            for(int i=0;i<V;i++){
                Edge e=cheapest[i];
                if(e==null)continue;
                
                int set1=find(e.src);
                int set2=find(e.dest);
                
                if(set1==set2)continue;
                System.out.println("Edge: " + e.src + "-" + e.dest + " Weight: " + e.weight);
                mw+=e.weight;
                union(set1,set2);
                numv--;
                added=true;
            }
            
            if(!added)break;
        }
        return mw;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int V = sc.nextInt();
        int E = sc.nextInt();

        List<Edge> edges = new ArrayList<>();
        for (int i = 0; i < E; i++) {
            edges.add(new Edge(sc.nextInt(), sc.nextInt(), sc.nextInt()));
        }

        int totalWeight = boruvkaMST(V, edges);
        System.out.println("Total Weight of MST: " + totalWeight);

        sc.close();
    }
}

class Edge {
    int src, dest, weight;
    Edge(int s, int d, int w) {
        src = s; dest = d; weight = w;
    }
}

```

## Output:

<img width="646" height="498" alt="image" src="https://github.com/user-attachments/assets/2f6c9ab1-c5c2-465b-bb8f-c15c06ecfcb0" />


## Result:
The program successfully implemented and the expected output is verified.
