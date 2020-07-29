```python
def bubble_sort(nums):
    for i in range(len(nums) - 1): 
        for j in range(len(nums) - i - 1):  
            if nums[j] > nums[j + 1]:
                nums[j], nums[j + 1] = nums[j + 1], nums[j]
    return nums
```

After first iteration, the largest will end up being the last "bubble up"
and then only iterate through the rest r-1
