# Two Pointers

Main Applications


# Filtering and Partitioning

You want to retain relatve ordering, remove duplicates, or move certain things in an array in a certain direction.

``` python
left = 0
for right in range(len(nums)):
    if condition(nums[right]):
        nums[left] = nums[right]
        left += 1
```



