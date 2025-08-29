# Longest Common Prefix

```Python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        # set the longest prefix to the length of the first string
        common_prefix = strs[0]
        common_prefix_length = len(common_prefix)

        for string in strs[1:]:
            """
            For every string in strs we will just 
            check if the first string is equivalent to the length 
            of the other string 
            and if not just keep decreasing the common prefix
            length down 

            If we get it to zero then there is no common prefix
            so we can just return 0 

            else we can just set it to this new length 
            """
            while common_prefix != string[0:common_prefix_length]:
                common_prefix_length -= 1
                if common_prefix_length == 0:
                    return "" 
            
                common_prefix = common_prefix[0:common_prefix_length]

        return common_prefix
```
Time: O(N^2) Since we need to iterate over every string for every string in the array<br>
Space: O(strs[0]) Since we do need to store the first string in the first variable<br>

Notes: This seems like an easy problem but u gotta like do this goofy method to like just check one by one for every char and make sure that the common prefix is actually the same which involves a bunch of slicing.
