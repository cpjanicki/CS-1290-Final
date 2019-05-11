# Maximum Length of Pair Chain

## Problem
You are given n pair of numbers. In every pair, the first number is always smaller than the second number.

Now, we define a pair (c,d) can follow another pair (a,b) if and only if b < c. Chain of pairs can be formed in this fashion. 

Given a set of pairs, find the length longest cahin which can be formed. You needn't use up all the given pairs. You can select pairs in any order

## Example 
```bash 
INPUT:[ [1,2], [2,3], [3,4] ] 
OUTPUT: 2

EXPLANATION: The longest chain is [1,2] -> [3,4]

NOTICE: 
  [1, 2]    1 < 2   TRUE the first number is always smaller than the second number! 
  [3, 4]    3 < 4   TRUE
  
  Since we can only define a pair IFF b < c 
  a = 1
  b = 2
  c = 3
  d = 4
  
  2 < 3 (b < c)   CHAIN OF PAIRS CAN BE FORMED! 

NOTE:
  1. The number of given pairs will be in the range [1,1000].
```
## Solution 
The problem is similar to "Longest Increasing Subsequence" problem.
If a chain of length n ends at some pairs[i], and pairs[i][1] < pairs [j][0], we can extend this
chain to a chain of length n+1.

Therefore, the following steps are used to solve this problem.

1) Sort pairs by the first coordinate, and use a new array variable(dp[i]) where the length of the longest chain ending at the 2D array of the pairs is stored (pairs[i]. 
2) Then run a modified pairs process where we compare the second element of already finalized pairs with the first element of the new pairs being constructed

*Since it is a list, I used Array list to solve this problem instead of HashMap. 

```java
 public int findLongestChain(int[][] pairs) {
        Arrays.sort(pairs, (a, b) -> a[0] - b[0]);
        int N = pairs.length;
        int[] dp = new int[N];  //LENGTH OF THE LONGEST CHAIN ENDING AT pairs[i]
        Arrays.fill(dp, 1);

        for (int j = 1; j < N; ++j) {
            for (int i = 0; i < j; ++i) { //When i < j
                if (pairs[i][1] < pairs[j][0])  // AND pairs[i][1] < pairs[j][0]
                    dp[j] = Math.max(dp[j], dp[i] + 1); // EXTEND THE CHAIN HERE and we have an answer!!!
            }
        }

        int ans = 0;
        for (int x: dp) if (x > ans) ans = x;
        return ans;
    }
```

