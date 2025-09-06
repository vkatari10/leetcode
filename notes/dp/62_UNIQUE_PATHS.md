# Unique Paths
```Python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:

        memo = {}

        def top_down(m, n):
            if (m, n) in memo:
                return memo[(m, n)]

            """
            For the base case we just check if either is 1 
            since if either is one then if we move down once more
            then there is only one more way to move which is the other
            direction that is not one
            """
            if m == 1 or n == 1:
                return 1

            """
            At every point in the grid we can reduce m or n by 1 
            by doing so then we will need to move in that direction 
            but at every point we can make two choices so we make 
            two calls here
            """
            result = helper(m - 1, n) + helper(m, n - 1) 
            memo[(m, n)] = result
            return result

        def bottom_up(m, n):

            

        return top_down(m, n)  

```
Time: O(n * m) Since we use the call stack and recursion to build the solution<br>
Space: O(n * m) Since we need to use the memo and call stack<br>

Notes: This can also be solved with bottom up DP
