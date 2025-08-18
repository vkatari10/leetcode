# Insert Interval 

```Python
class Solution:
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:

        res = []

        intervals.append(newInterval)

        intervals.sort(key=lambda x: x[0])

        prev = intervals[0]

        for ivl in intervals[1:]:

            if ivl[0] <= prev[1]:
                prev[1] = max(prev[1], ivl[1])
            else:
                res.append(prev)
                prev = ivl

        res.append(prev)

        return res
```
Time: O(NlogN) since we need to sort<br>
Space: O(N)/O(1) depending on how you view the return array, but it would be the size of the merged output which could be O(N)<br>

Notes: Equivalent to LC 56, not optimal solution<br>

```Python
class Solution:
    def insert(self, intervals: list[list[int]], newInterval: list[int]) -> list[list[int]]:
        res = []

        for interval in intervals:
            if newInterval[1] < interval[0]:
                res.append(newInterval)
                newInterval = interval
            elif newInterval[0] > interval[1]:
                res.append(interval)
            else:
                newInterval[0] = min(newInterval[0], interval[0])
                newInterval[1] = max(newInterval[1], interval[1])

        res.append(newInterval)
        return res
```
Time: O(N) no sorting...<br>
Space: O(N) for reasons above<br>

Notes: Since the input was already sorted we can take advantage of this to just append all previous starting intervals beforehand and then merge those that needed to be marged which avoids sorting all together. 


