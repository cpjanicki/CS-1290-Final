# Palindrome Substrings

## Problem
Given a string, your task is to count how many palindromic substrings in this string.

The substrings with different start indexes or end indexes are counted as different substrings even
they consist of same characters. 

NOTE: The input string length won't exceed 1000

## Example 
````bash 
INPUT: "abc"
OUTPUT: 3

EXPLANATION:
The three different palindromic strings are: "a" , "b" , "c" 

````

## Example 2
````
INPUT: "aaa"
OUTPUT: 6 

EXPLANATION:
The output is 6 because these are the 6 different plaindromic strings
"a" , "a" , "a", "aa" , "aa" , "aaa" 
````

## Solution 
N = length of the string
middle of palindrome: 2N - 1 Positions which can be either a letter or between two letters

For each center: Count all the palindromes that have the center.

If [a,b] is a palindromic interval, then [a+1. b-1] is too.
i.e. S[a], S[a+1], ... , S[b] is a palindrome 



````java
    public int countSubstrings(String S) {
        int N = S.length(), ans = 0;
        for (int center = 0; center <= 2*N-1; ++center) {
            int left = center / 2;
            int right = left + center % 2;
            while (left >= 0 && right < N && S.charAt(left) == S.charAt(right)) {
                ans++;
                left--;
                right++;
            }
        }
        return ans;
    }
````





