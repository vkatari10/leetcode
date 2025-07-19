# Delete middle Node of a Linked List


```Python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteMiddle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        
        if not head.next: # edge case if there is only one node in the input list
            return None

        trail = None
        slow = head
        fast = head

        while fast and fast.next: # find middle pointer and track node behind the middle pointer

            trail = slow
            slow = slow.next
            fast = fast.next.next

        trail.next = slow.next # delete node 
        return head
```
Time: O(n) Since we need to actally traverse the entire list by definition but the actual runtime is n / 2<br>
Space: O(1) Since we are just using pointers<br>

Notes: This question is actually easy but we need to make sure to remember how to find the middle node in a linked list which is the hardest part.
