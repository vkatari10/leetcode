# Meeting Rooms II 


```Python
"""
Definition of Interval:
class Interval(object):
    def __init__(self, start, end):
        self.start = start
        self.end = end
"""

class Solution:
    def minMeetingRooms(self, intervals: List[Interval]) -> int:
        if not intervals:
            return 0

        # sort each interval array into start and end times exclusivley
        starts = sorted(i.start for i in intervals)
        ends = sorted(i.end for i in intervals)


        s = e = 0 # l, r pointers
        max_rooms = 0
        rooms = 0

        while s < len(intervals):

            if starts[s] < ends[e]: # if the start time is before the next end time
                rooms += 1
                max_rooms = max(max_rooms, rooms) # inc max room 
                s += 1 # move to next meeting
            else:
                e += 1 # else move to next ending meeting
                rooms -= 1 # reduce rooms we need know since the other ended

        return max_rooms
```
Time: O(NlogN) Since we need to sort the input<br>
Space: O(N) since we seperate the start and end times into their own arrays<br>

Notes: This is another interval problem where we just find overlaps usually solved with like sorting and greedy techniques.
