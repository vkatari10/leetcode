# Merge Intervals

```Python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        res = []

        # sort by start time just like with any interval problem
        intervals.sort(key=lambda x: x[0])
        
        prev = intervals[0] # store first iterval (by start time)

        for interval in intervals[1:]:
            if interval[0] <= prev[1]: # if interval start time less than the end time
                prev[1] = max(prev[1], interval[1]) # modify the end time
            else: 
                res.append(prev) # append this final merged interval
                prev = interval # set prev to this new interval

        res.append(prev)

        return res
```
Time: O(NlogN) Since we sort input<br>
Space: O(N) for result array, potentially the sort algo if using merge sort<br>

Notes: Just like with any interval problem we need to sort but we use a trick here to track the last previous inverval to see if the next one matching some new criteria.
