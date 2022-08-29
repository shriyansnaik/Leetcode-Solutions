**Recursive**
```
def cutRod(self, price, n):
        
  def find(i, left):

      if i == 0:
          return left*price[i]

      take = 0
      if left >= i + 1: take = price[i] + find(i, left - (i + 1))

      not_take = find(i - 1, left)

      return max(take, not_take)

  return find(n - 1, n)
```        

**Memoization**
```
def cutRod(self, price, n):
  dp = {}
  def find(i, left):

      if i == 0:
          return left*price[i]

      if (i, left) in dp: return dp[(i, left)]

      take = 0
      if left >= i + 1: take = price[i] + find(i, left - (i + 1))

      not_take = find(i - 1, left)

      dp[(i, left)] = max(take, not_take)
      return dp[(i, left)]

  return find(n - 1, n)
```        

**OR**

```
def cutRod(self, price, n):
  dp = [[-1]*(n + 1) for _ in range(n)]
  def find(i, left):

      if i == 0:
          return left*price[i]

      if dp[i][left] != -1: return dp[i][left]

      take = 0
      if left >= i + 1: take = price[i] + find(i, left - (i + 1))

      not_take = find(i - 1, left)

      dp[i][left] = max(take, not_take)
      return dp[i][left]

  return find(n - 1, n)
```

**Tabulation**
```
def cutRod(self, price, n):
  dp = [[0]*(n + 1) for _ in range(n)]

  for left in range(n + 1):
      dp[0][left] = left*price[0]

  for i in range(1,n):
      for left in range(n + 1):
          take = 0
          if left >= i + 1: take = price[i] + dp[i][left - (i + 1)]

          not_take = dp[i - 1][left]

          dp[i][left] = max(take, not_take)

  return dp[n - 1][n]
```

**Space optimized**
```
def cutRod(self, price, n):
  prev = [0]*(n + 1)
  cur = [0]*(n + 1)

  for left in range(n + 1):
      prev[left] = left*price[0]

  for i in range(1,n):
      for left in range(n + 1):
          take = 0
          if left >= i + 1: take = price[i] + cur[left - (i + 1)]

          not_take = prev[left]

          cur[left] = max(take, not_take)

      prev = cur

  return prev[n]
```

**Even more space optimized**
```
def cutRod(self, price, n):
  prev = [0]*(n + 1)

  for left in range(n + 1):
      prev[left] = left*price[0]

  for i in range(1,n):
      for left in range(n + 1):
          take = 0
          if left >= i + 1: take = price[i] + prev[left - (i + 1)]

          not_take = prev[left]

          prev[left] = max(take, not_take)

  return prev[n]
```  
