**Recursive**
```
def findWays(num: List[int], tar: int) -> int:
    def find(i,sum1):
        
        if i == 0:
            if sum1 == 0 and num[i] == 0: return 2
            if sum1 == 0 or sum1 == num[i]: return 1
            return 0
                
        not_take = find(i - 1, sum1)
        take = 0
        if sum1 >= num[i]: take = find(i - 1, sum1 - num[i])
        
        return take + not_take
    
    return find(len(num) - 1, tar)
```    

**Memoized**
```
def findWays(num: List[int], tar: int) -> int:
    dp = {}
    def find(i,sum1):
        
        if i == 0:
            if sum1 == 0 and num[i] == 0: return 2
            if sum1 == 0 or sum1 == num[i]: return 1
            return 0
        
        if (i,sum1) in dp: return dp[(i,sum1)]
        
        not_take = find(i - 1, sum1)
        take = 0
        if sum1 >= num[i]: take = find(i - 1, sum1 - num[i])
        
        dp[(i,sum1)] = take + not_take
        return dp[(i,sum1)]
    
    return find(len(num) - 1, tar)
```

**Tabulation**
```
def findWays(num: List[int], tar: int) -> int:
    dp = [[0]*(tar + 1) for _ in range(len(num))]
    
    if num[0] == 0: dp[0][0] = 2
    else: 
        dp[0][0] = 1
        if num[0] <= tar: dp[0][num[0]] = 1
    
    for i in range(1,len(num)):
        for sum1 in range(tar + 1):
            not_take = dp[i - 1][sum1]
            take = 0
            if sum1 >= num[i]: take = dp[i - 1][sum1 - num[i]]

            dp[i][sum1] = take + not_take
    
    
    return dp[len(num) - 1][tar]
```

**Space Optimized**
```
def findWays(num: List[int], tar: int) -> int:
    prev = [0]*(tar + 1)
    
    if num[0] == 0: prev[0] = 2
    else: 
        prev[0] = 1
        if num[0] <= tar: prev[num[0]] = 1
    
    for i in range(1,len(num)):
        cur = [0]*(tar + 1)
        for sum1 in range(tar + 1):
            not_take = prev[sum1]
            take = 0
            if sum1 >= num[i]: take = prev[sum1 - num[i]]

            cur[sum1] = take + not_take
            
        prev = cur
    
    
    return prev[tar]
```
