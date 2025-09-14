# Traignle


Find the minimum path sum in a triangle

```Python
class Solution:
    def minimumTotal(self, triangle: List[List[int]]) -> int:
        """
        Example dp table being built up using example 1

        [0, 0, 0, 0, 0]
        [4, 0, 0, 0, 0]
        [4, 1, 0, 0, 0]
        [4, 1, 8, 0, 0]
        [4, 1, 8, 3, 0]
        First the cost of the bottom row is applied
        
        Then we go to the next row and looking down choose the min 
        from dp[i] or dp[i + 1]
        [7, 1, 8, 3, 0]
        [7, 6, 8, 3, 0]
        [7, 6, 10, 3, 0]

        Then the next row 
        [9, 6, 10, 3, 0]
        [9, 10, 10, 3, 0]

        Then dp[0] contains the top row cost that we add the end and we are done
        [11, 10, 10, 3, 0]

        Note this can be done in O(1) space using the triangle itself to modify 
        state
        """
        n = len(triangle) # number of rows
        dp = [0] * (n + 1)

        for row in triangle[::-1]: # working botom up on the triangle
            for i in range(len(row)): # for each element in the row 
                dp[i] = row[i] + min(dp[i], dp[i + 1]) # add this row value plus other choices at previous row iterations
        return dp[0]
```
Time: O(n^2)<br>
Space: O(n) or O(1) if using triangle directly as a dp table<br>

Notes: We work bottom up on the triangle since it makes building the dp table more easy. You can also do a O(1) solution by using the triangle itself to modify the state
