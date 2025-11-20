
# EX 5A 0/1 Knapsack Problem - Branch&Bound 
## DATE: 16-11-2025
## AIM:
To Write a Java program to solve 0/1 Knapsack problem using Branch and Bound Approach.
You are heading a college entrepreneurship cell that can invest in up to N student‑startups.

For each startup i you know: cost[i]  — the amount (in ₹ lakh) required to join the showcase profit[i] — the estimated profit (in ₹ lakh) you’ll gain if it succeeds You have a total budget of B ₹ lakh. Pick a subset of startups so that the sum of costs ≤ B and the sum of profits is maximised.

Because N can be as large as 50, a plain exhaustive search (2^N) is too slow.

The recommended approach is Branch & Bound with a fractional‑knapsack upper bound (but any algorithm that meets the constraints is accepted). 

Input Format

N

B

cost[1] cost[2] … cost[N]

profit[1] profit[2] … profit[N]

1 ≤ N ≤ 50

1 ≤ B ≤ 1 000 000

1 ≤ cost[i], profit[i] ≤ 10 000 

Output Format

maxProfit

For example:



## Algorithm
1. Read the number of startups N, total budget B, and arrays of costs and profits.
2. Sort the startups in decreasing order of profit-to-cost ratio to optimize bounding efficiency.
3. Use a fractional knapsack–based bound() function to compute an upper bound on achievable profit from any node.
4. Perform DFS exploring both inclusion and exclusion of each startup while pruning branches whose bound ≤ current best.
5. Track and update the maximum profit achievable without exceeding the budget.

#### Developed By: Mohamed Hameem Sajith J
#### Register Number: 212223240090

## Program:
```java
import java.util.*;

public class StartupInvestment {
    static int N, B;
    static int[] c, p;
    static double best = 0;

    static double bound(int idx, int cw, int cv) {
        if (cw >= B) return cv;
        double val = cv;
        int rem = B - cw;
        while (idx < N && c[idx] <= rem) {
            rem -= c[idx];
            val += p[idx];
            idx++;
        }
        if (idx < N) val += p[idx] * (rem / (double) c[idx]);
        return val;
    }

    static void dfs(int idx, int cw, int cv) {
        if (idx == N) {
            best = Math.max(best, cv);
            return;
        }
        if (cw + c[idx] <= B) {
            dfs(idx + 1, cw + c[idx], cv + p[idx]);
        }
        double ub = bound(idx + 1, cw, cv);
        if (ub > best) {
            dfs(idx + 1, cw, cv);
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        N = sc.nextInt();
        B = sc.nextInt();

        c = new int[N];
        p = new int[N];

        for (int i = 0; i < N; i++) c[i] = sc.nextInt();
        for (int i = 0; i < N; i++) p[i] = sc.nextInt();

        Integer[] order = new Integer[N];
        for (int i = 0; i < N; i++) order[i] = i;
        Arrays.sort(order, (i, j) -> Double.compare((double)p[j]/c[j], (double)p[i]/c[i]));

        int[] nc = new int[N], np = new int[N];
        for (int i = 0; i < N; i++) {
            nc[i] = c[order[i]];
            np[i] = p[order[i]];
        }
        c = nc; p = np;

        dfs(0, 0, 0);

        System.out.println((int)best);
    }
}
```

## Output:

<img width="357" height="231" alt="image" src="https://github.com/user-attachments/assets/6ca94105-7c61-48f6-bdf4-1976eee713ce" />


## Result:
The program successfully solved 0/1 Knapsack problem using branch & bound and output is verified. 
