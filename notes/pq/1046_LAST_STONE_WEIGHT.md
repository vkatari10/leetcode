# Last Stone Weight

Honestly read the problem description on leetcode. 
```Python
import heapq

class Solution:
    def lastStoneWeight(self, stones: List[int]) -> int:
        # NOTE: this solution is not clean but works

        pq = []
        '''
        Put every stone onto a PQ first 

        This gives us the stones sorted so we can 
        easily compare the first two highest weight stones
        '''
        for stone in stones:
            heapq.heappush(pq, -stone)


        while pq: # this may be a bad while condition 
            '''
            What we will do first is pop off the first two items

            we will then compare their weights, if they are equal then continue

            else take the diff of the stones

            We have two checks in place to account for if the pq is empty

            1. If we pop off one item (x) but the PQ is empty check
            if X doesnt exist just return 0 (no weight)

            2. If we have popped off two items but the pq is now empty, 
            just return zero because 2 equal weights = answer of 0
            '''
            x = heapq.heappop(pq)

            if not pq:
                x *= -1 
                return x if x is not None else 0

            y = heapq.heappop(pq)

            if x == y:
                if not pq:
                    return 0
                else:
                    continue
            else:
                x *= -1
                y = y + x

                if y > 0:
                    y *= -1
                '''
                Put back new stone weight back onto the PQ
                '''
                heapq.heappush(pq, y)
```
Time: O(NlogN) Since we need to store every item in the PQ and then pop off of it entirely<br>
Space: O(N) Since we need to store every item onto the PQ<br>

Notes: There are cleaner solutions that do the same exact thing as me but are like 10x cleaner so be sure to take a look at those.
