# Min Cost to connect all points

Given a list if points on a graph determine the min cost to connect all points.

```Python
import heapq

class Solution:
    def minCostConnectPoints(self, points: List[List[int]]) -> int:
        '''
        Given the nature of the problem is asking we can just use prims 
        to find the MST which is literally an algo to find the min
        cost to connect all points in graph
        '''

        n = len(points) # number of nodes (points)
        min_cost = 0 # ans
        visited = [False] * n # track visitied nodes (could use a set as well)
        pq = [(0, 0)] # PQ (cost, vertex)

        cache = {0:0} # cache (optional but reduces runtime)

        while pq:
            cost, u = heapq.heappop(pq) # -> distance and vertex

            if visited[u]: # if this vertex alr visited skip
                continue
            
            visited[u] = True # now mark this vertex as visited
            min_cost += cost # and add to ans

            for v in range(n): # check all other points in the graph 
                if not visited[v]: # if we have not seen that node calc distance and push
                    dist = abs(points[u][0] - points[v][0]) + abs(points[u][1] - points[v][1])

                    if dist < cache.get(v, float('inf')): # optional cache statment
                        # checking if dist less than that of v if not found put inf
                        cache[v] = dist
                        heapq.heappush(pq, (dist, v))

                    '''
                    The idea is that if we did not use the cache we just push every v
                    from this point we have not visitied however this is inefficnet
                    since we are pushing every node not visited yet onto the PQ

                    This makes the PQ persist for longer so we just check if the dist
                    is less than the cached value and if so then we should push it 

                    This keeps the PQ smaller than if we did not have this so it ends
                    up being ~NlogN 
                    '''

        return min_cost


```
Time: O(NlogN) Since we need to push every node onto the heap<br>
Space: O(N) Since we need a place to store every node<br>

Notes: Without the cahce this algo woud degrade to N^2logN since we could end up pushing every other node (v) for a given vertex (u) causing the heap to become bloated<br>
