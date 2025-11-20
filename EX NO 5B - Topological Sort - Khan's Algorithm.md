
# EX 5B Topological Sort - Khan's Algorithm
## DATE: 16-11-2025
## AIM:
To write a Java program to for given constraints.
Problem Description:
A software development team is preparing for a product release. The release consists of multiple tasks, each dependent on other tasks being completed first. You are to determine a valid order in which all tasks can be completed. If it's not possible due to cyclic dependencies, output that the release cannot be scheduled.

Each task is labeled from 0 to n-1. The dependencies are provided in the form of pairs [a, b] which means task a depends on task b.

Implement a program to find a valid task execution order using topological sort.

Input Format:

An integer n — number of tasks.

An integer m — number of dependencies.

m lines follow with two integers a and b — representing a depends on b.

Output Format:

If a valid order exists, print the task numbers in a possible execution order (space-separated).

If not, print "Release cannot be scheduled".

<img width="341" height="363" alt="image" src="https://github.com/user-attachments/assets/f0355541-4f66-49da-bcd3-171a799a7c1f" />

## Algorithm
1. Read the number of tasks and dependencies, and store all prerequisite pairs.  
2. Build an adjacency list graph and compute indegree for each task.  
3. Insert all tasks with indegree 0 into a queue.  
4. Process the queue by appending tasks to the order and reducing indegrees of dependent tasks.  
5. If all tasks are included in the order, print it; otherwise output that the release cannot be scheduled.  

#### Developed By: Mohamed Hameem Sajith J
#### Register Number: 212223240090

## Program:
```java
import java.util.*;

public class prog {

    public static List<Integer> findTaskOrder(int n, int[][] dependencies) {
        List<Integer> order = new ArrayList<>();
        List<List<Integer>> graph = new ArrayList<>();
        int[] indegree = new int[n];
        

        for (int i = 0; i < n; i++) {
            graph.add(new ArrayList<>());
        }
        

        for (int[] dep : dependencies) {
            graph.get(dep[1]).add(dep[0]);
            indegree[dep[0]]++;  
        }

        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            if (indegree[i] == 0) {
                q.offer(i);
            }
        }

        while (!q.isEmpty()) {  
            int curr = q.poll();
            order.add(curr);
            
            for (int neighbour : graph.get(curr)) {
                indegree[neighbour]--; 
                if (indegree[neighbour] == 0) {
                    q.offer(neighbour);
                }
            }
        }
        

        if (order.size() != n) {
            return null;
        }

        return order;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(); // number of tasks
        int m = sc.nextInt(); // number of dependencies

        int[][] dependencies = new int[m][2];
        for (int i = 0; i < m; i++) {
            dependencies[i][0] = sc.nextInt(); // task
            dependencies[i][1] = sc.nextInt(); // prerequisite
        }

        List<Integer> result = findTaskOrder(n, dependencies);

        if (result == null) {
            System.out.println("Release cannot be scheduled");
        } else {
            for (int task : result) {
                System.out.print(task + " ");
            }
        }
    }
}
```

## Output:

<img width="697" height="536" alt="image" src="https://github.com/user-attachments/assets/dce883cb-ca01-4ecd-9313-8920c4e9bee9" />


## Result:
The program successfully implemented and the expected output is verified.
