**Recursion**
```
def knapSack(self,W, wt, val, n):
  def fill(i, left):
      if left == 0: return 0
      if i == 0:
          if left >= wt[i]: return val[i]
          return 0

      take = 0
      if left >= wt[i]: take = val[i] + fill(i - 1, left - wt[i])
      not_take = fill(i - 1, left)

      return max(take, not_take)

  return fill(n - 1, W)
```

**Memoization**
```
def knapSack(self,W, wt, val, n):
  dp = [[-1]*(W+1) for _ in range(n)]
  def fill(i, left):
      if left == 0: return 0
      if i == 0:
          if left >= wt[i]: return val[i]
          return 0

      if dp[i][left] != -1: return dp[i][left]
      take = 0
      if left >= wt[i]: take = val[i] + fill(i - 1, left - wt[i])
      not_take = fill(i - 1, left)

      dp[i][left] = max(take, not_take)
      return dp[i][left]

  return fill(n - 1, W)
```  

**Tabulation**
```
def knapSack(self,W, wt, val, n):
  dp = [[0]*(W+1) for _ in range(n)]

  for i in range(wt[0], W + 1): dp[0][i] = val[0]

  for i in range(1, n):
      for left in range(W + 1):
          take = 0
          if left >= wt[i]: take = val[i] + dp[i - 1][left - wt[i]]
          not_take = dp[i - 1][left]

          dp[i][left] = max(take, not_take)

  return dp[n - 1][W]
```  

**Space Optimized**
```
def knapSack(self,W, wt, val, n):
  prev = [0]*(W+1)

  for i in range(wt[0], W + 1): prev[i] = val[0]

  for i in range(1, n):
      cur = [0]*(W+1)
      for left in range(W + 1):
          take = 0
          if left >= wt[i]: take = val[i] + prev[left - wt[i]]
          not_take = prev[left]

          cur[left] = max(take, not_take)
      prev = cur        
  return prev[W]
```        

**OR**

```
def knapSack(self,W, wt, val, n):
  prev = [0]*(W+1)

  for i in range(wt[0], W + 1): prev[i] = val[0]

  for i in range(1, n):
      cur = [0]*(W+1)
      for left in range(W, -1, -1):
          take = 0
          if left >= wt[i]: take = val[i] + prev[left - wt[i]]
          not_take = prev[left]

          cur[left] = max(take, not_take)
      prev = cur        
  return prev[W]
```        
       
**Even more space-optimized 🤩**       
```
def knapSack(self,W, wt, val, n):
  prev = [0]*(W+1)

  for i in range(wt[0], W + 1): prev[i] = val[0]

  for i in range(1, n):
      for left in range(W, -1, -1):
          take = 0
          if left >= wt[i]: take = val[i] + prev[left - wt[i]]
          not_take = prev[left]

          prev[left] = max(take, not_take)
  return prev[W]
```        
