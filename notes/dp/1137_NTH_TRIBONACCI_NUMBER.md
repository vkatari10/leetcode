# N-th Tribonacci Number

```Python
class Solution:
    def tribonacci(self, n: int) -> int:
        memo = {}

        if n == 0:
            return 0

        def helper(n):
            if n in memo:
                return memo[n]
            if n == 0:
                return 0
            elif n == 2 or n == 1:
                return 1
            else:
                memo[n] = helper(n - 1) + helper(n - 2) + helper(n - 3)
                return memo[n]

        def bottom_up(n):
            if n == 0:
                return 0
            elif n in (1, 2):
                return 1
                
            dp = [0] * (n + 1)
            dp[0] = 0
            dp[1] = dp[2] = 1

            for i in range(3, len(dp)):
                dp[i] = dp[i - 1] + dp[i - 2] + dp[i - 3]

            return dp[n]

        def bottom_up_const(n):
            a, b, c = 0, 1, 1

            for i in range(3, n + 1):
                d = a + b + c # next trib
                a, b, c = b, c, d # shift to next 3 numbers
            return c # since  c contains the last d value which is n

        return bottom_up(n)
```
Time: O(N) with optimal solution<br>
Space: O(N) or O(1) depending on solution<br>

Notes: This shows the 3 different ways that we can apporach a DP problem
