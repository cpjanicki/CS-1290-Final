# Perfect Squares

## Problem
Given a positive integer n, find the least number of perfect square numbers (such as, 1,4,9,16,...) which sum to n.

In other words, you want to find the best way to add up a sum using the least possible numbers added.

RECALL that perfect square numbers are the numbers that can be square rooted perfectly such as the square root of 16 is 4

## Example 
```bash 
INPUT: n = 12

Since the input is 12, you want to add up to 12 using the least number of perfect square numbers.

OUTPUT: 3

EXPLANATION:
12 = 4 + 4 + 4              TRUE (Since this uses the least number of perfect square numbers, the answer is 3)
```
## Example 2
```bash
INPUT: n = 13
OUTPUT: 2

EXPLANATION 
13 = 4 + 9       TRUE(THERSE ARE THE ONLY TWO perfect square root numbers that can be added to 13 which is better than adding all of them using ones) 
```

## Solution 

The idea to this solution should be straight-forward. We start from 1 and go until a number whos sqaure is smaller than or equals to n. For every number k, we recursively call for n-k times. Therefore, if n =1 and k^2 <= n.

The code is a simple recursive program to find the minimum number of squares whose sum is equal to a given number

```java
class squares 
{ 
    // Returns count of minimum squares that sum to n 
    static int getMinSquares(int n) 
    { 
  
       // We need to add a check here for n. If user enters 0 or 1 or 2  
       // the below array creation will go OutOfBounds. 
       if(n<=3) 
         return n; 
  
        // Create a dynamic programming table 
        // to store sq 
        int dp[] = new int[n+1]; 
       
        // getMinSquares table for base case entries 
        dp[0] = 0; 
        dp[1] = 1; 
        dp[2] = 2; 
        dp[3] = 3; 
       
        // getMinSquares rest of the table using recursive 
        // formula 
        for (int i = 4; i <= n; i++) 
        { 
            // max value is i as i can always be represented 
            // as 1*1 + 1*1 + ... 
            dp[i] = i; 
       
            // Go through all smaller numbers to 
            // to recursively find minimum 
            for (int x = 1; x <= i; x++) { 
                int temp = x*x; 
                if (temp > i) 
                    break; 
                else dp[i] = Math.min(dp[i], 1+dp[i-temp]); 
            } 
        } 
       
        // Store result and free dp[] 
        int res = dp[n]; 
       
        return res; 
    } 
    public static void main(String args[]) 
    { 
       System.out.println(getMinSquares(6)); 
    } 
}
```
