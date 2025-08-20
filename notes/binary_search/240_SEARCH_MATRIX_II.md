# Search 2D Matrix II

```Python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        
        r, c = 0, len(matrix[0]) - 1

        while r < len(matrix) and c >= 0:

            if matrix[r][c] == target:
                return True
            elif matrix[r][c] > target:
                c -= 1
            elif matrix[r][c] < target: 
                r += 1
            
        return False
```
Time: O(N) or O(r + c)<br>
Space: O(1)<br>

Notes: Instead of a double binary search first on the first row then down that column we can just start at the top right corner and then exploit the structure of the matrix
