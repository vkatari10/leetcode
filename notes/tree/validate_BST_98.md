# Validate BST

Determine if a given BST violates the ordering rule.



```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:


        nodes = []

        def inorder(root):
    
            if not root:
                return 

            inorder(root.left)
      
            nodes.append(root.val)
            inorder(root.right)

        inorder(root)
        
        for i in range(len(nodes) - 1):
            if nodes[i] >= nodes[i + 1]:
                return False

        return True
            
        
```
Time: O(n) To perform inorder traversal<br>
Space: O(n) To store all nodes in<br>

Notes: This is a pretty simple solution since we want to check if its a BST or not we can just do the in order traversal of the BST which gives the nodes of the tree in sorted order and all we have to do is check if the resulting nodes are in order if not we know it is not a BST then. 












