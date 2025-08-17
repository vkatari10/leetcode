# Valid Soddoku

Given a board with some filled Sodoku elements, find if the board is valid or not

```Python
from collections import defaultdict

class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        rows = defaultdict(set)
        cols = defaultdict(set)
        boxes = defaultdict(set)

        for row in range(9):
            for col in range(9):

                if board[row][col] == ".":
                    continue

                ele = board[row][col]

                """
                Boxes is just telling us which main box the element is located in since 
                we just divide by the size of the entire board, therefore we can check 
                for repeated elements inside a certain box
                """

                # again this is a hashmap so we are just storing the tuple as a key
                if ele in rows[row] or ele in cols[col] or ele in boxes[(row // 3, col // 3)]: 
                    return False

                rows[row].add(ele) # defaultdict so we can just do add
                cols[col].add(ele)
                boxes[(row // 3, col // 3)].add(ele)


        return True
```
Time: O(1) Since board size is fixed<br>
Space: O(1) Since board size is fixed<br>

Notes: We use the box trick by using `// 3` to locate where the element is on the board. We also use defaultdict so we can just add values rather than using `.get()`
