Difficulty : Medium 

>Given an array of strings nums containing n unique binary strings each of length n, return a binary string of length n that does not appear in nums. If there are multiple answers, you may return any of them.
>
>>Example 1:    
>>
>>Input: nums = ["01","10"]  
>>Output: "11"  
>>Explanation: "11" does not appear in nums. "00" would also be correct.

```python
class Solution:
    def findDifferentBinaryString(self, nums: List[str]) -> str:
        res = []
        for i in range(len(nums)):
            if nums[i][i] == '1':
                res.append('0')
            else:
                res.append('1')
        return "".join(res)
```
