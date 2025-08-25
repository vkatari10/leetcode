# Diagonal Traverse

```Python
class Solution:
    def findDiagonalOrder(self, mat: List[List[int]]) -> List[int]:

        res = []
        
        r = 0
        c = 0

        up = True

        m, n = len(mat), len(mat[0])

        for _ in range(m * n):
            res.append(mat[r][c])
            """
            we check the boundaries exactly at the point that we need to adjust
            which means that no >= m/n or <= 0 should be used but the exact comparison 
            should be done

            we use Up to tell if we move diagonal up or not

            The n / m checks should come before the == 0 checks since we will  
            slip out of bounds if we do not check those bounds
            """

            if up: # moving up right
                
                if c == n - 1: # if our col jumps too far adjust to new row
                    r += 1
                    up = False
                elif r == 0: # if we go to far go to the next col 
                    c += 1
                    up = False
                else: # regular up right movement
                    r -= 1
                    c += 1

            else: # moving down left

                if r == m - 1: # if we hit the bottom row move to next col
                    #   primed to go back up on the next loop iteration 
                    c += 1
                    up = True
                elif c == 0: # if we hit zero col then adjust to next row 
                    r += 1
                    up = True
                else: # regular up left movement
                    r += 1
                    c -= 1

        return res
                


                
```
Time: O(n * m)<br>
Space: O(1)/O(N) if we count the result array or not<br>

Notes: This seems easy on paper but the bounds checking is the hardest since we cannot use `<=` or `>=` in this case but bounce exactly at the point that we hit at the ends to move up and down. Also the order of the checks are very important since if we do not check the `== m - 1` or `== n - 1` this approach does not work since we swtich directions in between loop iterations.
