
# EX 5D Flower Planting.
## DATE: 16-11-2025
## AIM:
To write a Java program to for given constraints.
You are given n gardens, labelled from 1 to n.

You also have a list called paths, where each element paths[i] = [xi, yi] represents a bidirectional road connectingthe  garden xi and garden yi.

You want to plant one flower in each garden, and there are exactly 4 types of flowers labelled as 1, 2, 3, and 4.

Your goal is to plant flowers such that:

No two connected gardens (i.e., connected via a path) have the same flower type.

Return any valid flower assignment as an array where:

answer[i] is the flower type planted in the (i+1) ᵗʰ garden

It is guaranteed that:

No garden is connected to more than 3 other gardens

A valid flower assignment always exists

<img width="177" height="292" alt="image" src="https://github.com/user-attachments/assets/36aa40cb-1cdd-4746-b1a6-fc51ce6e96aa" />

## Algorithm
1. Build a graph where each garden is connected to its neighboring gardens.  
2. Create an array to store the flower type chosen for each garden.  
3. For every garden, check which flower types (1–4) are already used by its neighbors.  
4. Assign the first available flower type that is not used by adjacent gardens.  
5. Return the final flower assignment for all gardens.

#### Developed By: Mohamed Hameem Sajith J
#### Register Number: 212223240090
 

## Program:
```java
import java.util.*;

public class GardenFlowerPlanner {

    public static int[] assignFlowers(int n, int[][] paths) {
        @SuppressWarnings("unchecked")
        List<Integer>[] g= new ArrayList[n];
        // Type Your Code Here.
        for(int i=0;i<n;i++)g[i]=new ArrayList<>();
        for(int[] p:paths){
            g[p[0]-1].add(p[1]-1);
            g[p[1]-1].add(p[0]-1);
        }
        int[] ans= new int[n];
        for(int i=0;i<n;i++){
            boolean[] used = new boolean[5];
            for(int j:g[i])used[ans[j]]=true;
            for(int f=1;f<=4;f++)if(!used[f]){ans[i]=f;break;}
        }
        return ans;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt(); 
        int m = sc.nextInt(); 

        int[][] paths = new int[m][2];
        for (int i = 0; i < m; i++) {
            paths[i][0] = sc.nextInt();
            paths[i][1] = sc.nextInt();
        }
        int[] result = assignFlowers(n, paths);

        for (int flower : result) {
            System.out.print(flower + " ");
        }
        System.out.println();
    }
}

```

## Output:

<img width="416" height="459" alt="image" src="https://github.com/user-attachments/assets/1f093039-99e6-45ff-a565-08475b7f0d51" />


## Result:
The program successfully implemented and the expected output is verified.
