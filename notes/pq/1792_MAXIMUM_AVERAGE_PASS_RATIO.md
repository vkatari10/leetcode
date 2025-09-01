# Maximum Average Pass Ration 
```Python
import heapq

class Solution:
    def maxAverageRatio(self, classes: List[List[int]], extraStudents: int) -> float:
        """
        Instead of ranking the by the current ratio and using a min heap 
        we will rank using a max heap of the potential gains from adding a new 
        student to maximize the total ratio
        """

        def gain(n, d): # definition of gain from one more student 
            return (n + 1) / (d + 1) - n / d

        # heap construction
        heap = [(-gain(n, d), n, d) for n, d in classes]
        heapq.heapify(heap)

        for _ in range(extraStudents):
            # pop off class with highest potential gain 
            # recalc and repush 
            g, n, d = heapq.heappop(heap)
            n, d = n + 1, d + 1
            heapq.heappush(heap, (-gain(n, d), n, d))
        
        # sum up heap ratios
        total = sum(n / d for _, n, d in heap)
        return total / len(classes)
```
Time: O(NlogN) since we are using a heap<br>
Space: O(N) since we need to store every class<br>

Notes: This is obviously a greedy solution but the hard part is figuring out how we determine which next class deserves the next student, which is actually the potential gain from the next student not the current ratio of the class. 
