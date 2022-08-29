**Recursion**
```
def unboundedKnapsack(n, w, profit, weight):
    
    def find(i, left):
        
        if i == 0:
            return (left//weight[0])*profit[0]
        
        take = 0
        if left >= weight[i]: take = profit[i] + find(i, left - weight[i])
        not_take = find(i - 1, left)
        
        return max(take, not_take)
    
    return find(n - 1, w)
```

**Memoization**
```
def unboundedKnapsack(n, w, profit, weight):
    
  dp = {}
  def find(i, left):

      if i == 0:
          return (left//weight[0])*profit[0]

      if (i, left) in dp: return dp[(i, left)]

      take = 0
      if left >= weight[i]: take = profit[i] + find(i, left - weight[i])
      not_take = find(i - 1, left)

      dp[(i, left)] = max(take, not_take)
      return dp[(i, left)]

  return find(n - 1, w)
```  

**OR**

```
dp = [[-1]*(w + 1) for _ in range(n)]
  def find(i, left):

      if i == 0:
          return (left//weight[0])*profit[0]
          return 0

      if dp[i][left] != -1: return dp[i][left]

      take = 0
      if left >= weight[i]: take = profit[i] + find(i, left - weight[i])
      not_take = find(i - 1, left)

      dp[i][left] = max(take, not_take)
      return dp[i][left]

  return find(n - 1, w)
```

**Tabulation**
```
def unboundedKnapsack(n, w, profit, weight):
    
  dp = [[0]*(w + 1) for _ in range(n)]

  for left in range(w + 1):
      dp[0][left] = (left//weight[0])*profit[0]

  for i in range(1,n):
      for left in range(w + 1):
          take = 0
          if left >= weight[i]: take = profit[i] + dp[i][left - weight[i]]
          not_take = dp[i - 1][left]

          dp[i][left] = max(take, not_take)

  return dp[n - 1][w]
```  

**Space Optimized**
```
def unboundedKnapsack(n, w, profit, weight):
    
  prev = [0]*(w + 1)
  cur = [0]*(w + 1)

  for left in range(w + 1):
      prev[left] = (left//weight[0])*profit[0]

  for i in range(1,n):
      for left in range(w + 1):
          take = 0
          if left >= weight[i]: take = profit[i] + cur[left - weight[i]]
          not_take = prev[left]

          cur[left] = max(take, not_take)
      prev = cur
  return prev[w]
```         
       
**Even more space-optimized 🤩**       
```
def unboundedKnapsack(n, w, profit, weight):
    
    prev = [0]*(w + 1)
    
    for left in range(w + 1):
        prev[left] = (left//weight[0])*profit[0]
        
    for i in range(1,n):
        for left in range(w + 1):
            take = 0
            if left >= weight[i]: take = profit[i] + prev[left - weight[i]]
            not_take = prev[left]

            prev[left] = max(take, not_take)
 
    return prev[w]
```        
