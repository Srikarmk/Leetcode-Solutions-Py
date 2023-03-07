Difficulty : Hard 

>Given an array of integers arr, you are initially positioned at the first index of the array.
>
>In one step you can jump from index i to index:
>
>i + 1 where: i + 1 < arr.length.
>i - 1 where: i - 1 >= 0.
>j where: arr[i] == arr[j] and i != j.
>Return the minimum number of steps to reach the last index of the array.
>
>Notice that you can not jump outside of the array at any time.
>
>>Example 1:  
>>
>>Input: arr = [100,-23,-23,404,100,23,23,23,3,404]  
>>Output: 3  
>>Explanation: You need three jumps from index 0 --> 4 --> 3 --> 9. Note that index 9 is the last index of the array.  

```python
class Solution:
  def minJumps(self, arr: List[int]) -> int:
    n = len(arr)
    # {num: indices}
    graph = collections.defaultdict(list)
    steps = 0
    q = collections.deque([0])
    seen = {0}

    # Create graph where keys are elements and values are their indices in arr
    for i, a in enumerate(arr):
      graph[a].append(i)

    # BFS
    while q:
      # Process all nodes at current level
      for _ in range(len(q)):
        i = q.popleft()
        # If last index is reached, return number of steps
        if i == n - 1:
          return steps
        seen.add(i)
        u = arr[i]
        # Add adjacent indices to graph
        if i + 1 < n:
          graph[u].append(i + 1)
        if i - 1 >= 0:
          graph[u].append(i - 1)
        # Process all adjacent nodes
        for v in graph[u]:
          if v in seen:
            continue
          q.append(v)
        # Clear indices in graph to avoid revisiting
        graph[u].clear()
      steps += 1
```      
